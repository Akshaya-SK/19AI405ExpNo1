<h1>ExpNo 1 :Developing AI Agent with PEAS Description</h1>
<h3>Name: Saravanan N</h3>
<h3>Register Number/Staff Id: TSML006</h3>

<h3>AIM:</h3>
<p>To find the PEAS description for the given AI problem and develop an AI agent.</p>

<h3>Theory</h3>
<h3>Medicine prescribing agent:</h3>
<p>This agent prescribes medicine for fever (temperature greater than 98.5°F), which is considered unhealthy. The agent receives temperature input and checks patients in two hospital rooms. It must consider room location and whether a patient is unhealthy. The agent moves between rooms to diagnose and treat patients. Each treatment increases performance, while each room switch decreases performance. The agent’s goal is to effectively prescribe medicine.</p>

<hr>

<h3>PEAS DESCRIPTION:</h3>
<table border="1" cellspacing="0" cellpadding="6">
  <tr>
    <th>Agent Type</th>
    <th>Performance</th>
    <th>Environment</th>
    <th>Actuators</th>
    <th>Sensors</th>
  </tr>
  <tr>
    <td>Medicine prescribing agent</td>
    <td>Treating unhealthy, agent movement</td>
    <td>Rooms, Patients</td>
    <td>Medicine, Treatment</td>
    <td>Location, Temperature of patient</td>
  </tr>
</table>

<hr>

<h3>DESIGN STEPS</h3>
<h4>STEP 1: Identifying the input</h4>
<p>Temperature from patients, Room location.</p>

<h4>STEP 2: Identifying the output</h4>
<p>Prescribe medicine if the patient has a fever.</p>

<h4>STEP 3: Developing the PEAS description</h4>
<p>Defined as above using Performance, Environment, Actuators, and Sensors.</p>

<h4>STEP 4: Implementing the AI agent</h4>
<p>The agent treats unhealthy patients and moves between rooms to diagnose others.</p>

<h4>STEP 5: Measuring performance</h4>
<p>+1 for each treatment, -1 for each movement between rooms.</p>

<h3>PROGRAM</h3>
<div style="background:#f4f4f4;border:1px solid #ccc;padding:10px;overflow-x:auto;white-space:pre;font-family:monospace;">
<pre><code>
import random
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

environment = {
    "Room1": Patient(random.uniform(97.0, 101.0)),
    "Room2": Patient(random.uniform(97.0, 101.0))
}

agent = MedicinePrescribingAgent(environment)
agent.run()
</code></pre>
</div>

<h3>OUTPUT</h3>
<!-- Replace the src link with your actual image URL -->
<img src="https://github.com/user-attachments/assets/dc761611-d0b7-458c-a600-fe535eb3e975/your-output-image.png" alt="Program Output" style="width:100%;max-width:600px;border:1px solid #ccc;">
