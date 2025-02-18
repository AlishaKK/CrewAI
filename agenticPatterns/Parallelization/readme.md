*Parallelization and Aggregation with the and_ Decorator*

Below is an example that demonstrates how to use the and_ decorator in CrewAI Flows. In this example, two tasks run in parallel, and we use and_ to wait until both tasks complete before combining their outputs. The scenario simulates generating two separate creative outputs (a slogan and a tagline) for a futuristic brand, and then the flow aggregates both results into a single combined message.


from crewai.flow.flow import Flow, start, listen, and_
from litellm import completion

class AndAggregationFlow(Flow):
    model = "gpt-4o-mini"

    @start()
    def generate_slogan(self):
        # This task generates a creative slogan.
        response = completion(
            model=self.model,
            messages=[{
                "role": "user",
                "content": "Generate a creative slogan for a futuristic brand."
            }]
        )
        slogan = response["choices"][0]["message"]["content"].strip()
        print("Slogan generated:", slogan)
        return slogan

    @start()
    def generate_tagline(self):
        # This task generates a creative tagline.
        response = completion(
            model=self.model,
            messages=[{
                "role": "user",
                "content": "Generate a creative tagline for a futuristic brand."
            }]
        )
        tagline = response["choices"][0]["message"]["content"].strip()
        print("Tagline generated:", tagline)
        return tagline

    @listen(and_(generate_slogan, generate_tagline))
    def combine_outputs(self, outputs):
        # The `and_` decorator ensures this method is called only when both tasks complete.
        # 'outputs' is a tuple containing the outputs of generate_slogan and generate_tagline.
        slogan, tagline = outputs
        combined = f"Combined Output: Slogan - '{slogan}' | Tagline - '{tagline}'"
        print("Aggregated Combined Output:", combined)
        return combined

if __name__ == "__main__":
    flow = AndAggregationFlow()
    final_output = flow.kickoff()
    print("Final Output of the Flow:")
    print(final_output)

