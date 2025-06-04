<h1>ExpNo 1 :Developing AI Agent with PEAS Description</h1>
<h3>Name: Saravanan N</h3>
<h3>Register Number/Staff Id: TSML006</h3>


<h3>AIM:</h3>
<br>
<p>To find the PEAS description for the given AI problem and develop an AI agent.</p>
<br>
<h3>Theory</h3>
<h3>Medicine prescribing agent:</h3>
<p>Such this agent prescribes medicine for fever (greater than 98.5 degrees) which we consider here as unhealthy, by the user temperature input, and another environment is rooms in the hospital (two rooms). This agent has to consider two factors one is room location and an unhealthy patient in a random room, the agent has to move from one room to another to check and treat the unhealthy person. The performance of the agent is calculated by incrementing performance and each time after treating in one room again it has to check another room so that the movement causes the agent to reduce its performance. Hence, agents prescribe medicine to unhealthy.</p>
<hr>
<h3>PEAS DESCRIPTION:</h3>
<table>
  <tr>
    <td><strong>Agent Type</strong></td>
    <td><strong>Performance</strong></td>
     <td><strong>Environment</strong></td>
    <td><strong>Actuators</strong></td>
    <td><strong>Sensors</strong></td>
  </tr>
    <tr>
    <td><strong>Medicine prescribing agent</strong></td>
    <td><strong>Treating unhealthy, agent movement</strong></td>
     <td><strong>Rooms, Patient</strong></td>
    <td><strong>Medicine, Treatment</strong></td>
    <td><strong>Location, Temperature of patient</strong></td>
  </tr>
</table>
<hr>
<H3>DESIGN STEPS</H3>
<h3>STEP 1:Identifying the input:</h3>
<p>Temperature from patients, Location.</p>
<h3>STEP 2:Identifying the output:</h3>
<p>Prescribe medicine if the patient in a random has a fever.</p>
<h3>STEP 3:Developing the PEAS description:</h3>
<p>PEAS description is developed by the performance, environment, actuators, and sensors in an agent.</p>
<h3>STEP 4:Implementing the AI agent:</h3>
<p>Treat unhealthy patients in each room. And check for the unhealthy patients in random room</p>
<h3>STEP 5:</h3>
<p>Measure the performance parameters: For each treatment performance incremented, for each movement performance decremented</p>

<h3>PROGRAM</h3>
```
import random

# Define constants
ROOMS = ["Room1", "Room2"]
FEVER_THRESHOLD = 98.5

class Patient:
    def __init__(self, temperature):
        self.temperature = temperature
        self.treated = False

    def is_unhealthy(self):
        return self.temperature > FEVER_THRESHOLD and not self.treated

class MedicinePrescribingAgent:
    def __init__(self, environment):
        self.environment = environment  # {room_name: Patient}
        self.current_room = random.choice(ROOMS)
        self.performance = 0

    def sense(self):
        patient = self.environment[self.current_room]
        return self.current_room, patient.temperature

    def treat(self):
        patient = self.environment[self.current_room]
        if patient.is_unhealthy():
            print(f"Treating patient in {self.current_room} with temperature {patient.temperature}")
            patient.treated = True
            self.performance += 1
        else:
            print(f"No treatment needed in {self.current_room} (Temp: {patient.temperature})")

    def move(self):
        next_room = ROOMS[1] if self.current_room == ROOMS[0] else ROOMS[0]
        print(f"Moving from {self.current_room} to {next_room}")
        self.current_room = next_room
        self.performance -= 1

    def run(self, cycles=4):
        for _ in range(cycles):
            print("\n--- New Cycle ---")
            room, temp = self.sense()
            self.treat()
            self.move()

        print(f"\nFinal Performance Score: {self.performance}")

# Initialize environment with patients having random temperatures
environment = {
    "Room1": Patient(random.uniform(97.0, 101.0)),
    "Room2": Patient(random.uniform(97.0, 101.0))
}

# Create and run the agent
agent = MedicinePrescribingAgent(environment)
agent.run()
```
