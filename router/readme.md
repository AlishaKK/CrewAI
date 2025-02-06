
**Workflow: Routing**


Routing classifies an input and directs it to a specialized followup task. This workflow allows for separation of concerns, and building more specialized prompts. Without this workflow, optimizing for one kind of input can hurt performance on other inputs.

![image](https://github.com/user-attachments/assets/46266dd0-5c67-4c6e-9306-56cf18b9641d)

import random

from crewai.flow.flow import Flow, listen, router, start

from pydantic import BaseModel


class ExampleState(BaseModel):

    success_flag: bool = False
    

class RouterFlow(Flow[ExampleState]):


    @start()
    def start_method(self):
        print("Starting the structured flow")
        random_boolean = random.choice([True, False])
        self.state.success_flag = random_boolean

    @router(start_method)
    def second_method(self):
        if self.state.success_flag:
            return "success"
        else:
            return "failed"

    @listen("success")
    def third_method(self):
        print("Third method running")

    @listen("failed")
    def fourth_method(self):
        print("Fourth method running")


flow = RouterFlow()

flow.kickoff()
