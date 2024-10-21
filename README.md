<H3>Enter Name</H3> ADHITHIYAN K

<H3>Enter Register No.</H3>212222230006

<H3>Experiment 2</H3>

<H3>Date</H3>
<h1 align =center>Implementation of Exact Inference Method of Bayesian Network</h1>

## Aim:
To implement the inference Burglary P(B| j,⥗m) in alarm problem by using Variable Elimination method in Python.

## Algorithm:

Step 1: Define the Bayesian Network structure for alarm problem with 5 random variables, Burglary,Earthquake,John Call,Mary Call and Alarm.<br>


Step 2: Define the Conditional Probability Distributions (CPDs) for each variable using the TabularCPD class from the pgmpy library.<br>
Step 3: Add the CPDs to the network.<br>

Step 4: Initialize the inference engine using the VariableElimination class from the pgmpy library.<br>

Step 5: Define the evidence (observed variables) and query variables.<br>

Step 6: Perform exact inference using the defined evidence and query variables.<br>
Step 7: Print the results.<br>

## Program :

```
# Importing Library
from pgmpy.models import BayesianNetwork
from pgmpy.inference import VariableElimination
```
```
# Defining network structure

alarm_model = BayesianNetwork(
    [
        ("Burglary", "Alarm"),
        ("Earthquake", "Alarm"),
        ("Alarm", "JohnCalls"),
        ("Alarm", "MaryCalls"),
    ]
)

# Defining the parameters using CPT
from pgmpy.factors.discrete import TabularCPD

cpd_burglary = TabularCPD(
    variable="Burglary", variable_card=2, values=[[0.999], [0.001]]
)
cpd_earthquake = TabularCPD(
    variable="Earthquake", variable_card=2, values=[[0.998], [0.002]]
)
cpd_alarm = TabularCPD(
    variable="Alarm",
    variable_card=2,
    values=[[0.999, 0.71, 0.06, 0.05], [0.001, 0.29, 0.94, 0.95]],
    evidence=["Burglary", "Earthquake"],
    evidence_card=[2, 2],
)
cpd_johncalls = TabularCPD(
    variable="JohnCalls",
    variable_card=2,
    values=[[0.95, 0.1], [0.05, 0.9]],
    evidence=["Alarm"],
    evidence_card=[2],
)
cpd_marycalls = TabularCPD(
    variable="MaryCalls",
    variable_card=2,
    values=[[0.99, 0.3], [0.01, 0.7]],
    evidence=["Alarm"],
    evidence_card=[2],
)

# Associating the parameters with the model structure
alarm_model.add_cpds(
    cpd_burglary, cpd_earthquake, cpd_alarm, cpd_johncalls, cpd_marycalls
)
```
```
alarm_model.check_model()
inference=VariableElimination(alarm_model)
query='Burglary'
evidence={"JohnCalls":1,"MaryCalls":0}
res = inference.query(variables=[query], evidence=evidence)
print(res)

evidence2={"JohnCalls":1,"MaryCalls":1}
res2=inference.query(variables=[query],evidence=evidence2)
print(res2)
```


## Output :

![365802132-924b33d1-5328-4f8a-8479-1c8389052591](https://github.com/user-attachments/assets/9f5cca9f-5b0c-41c2-af4a-21bcbebf830f)

![365802794-7513104b-d540-40d3-b9a1-6d4a11b91fd5](https://github.com/user-attachments/assets/a43a9a70-aecb-4049-9d60-dcd0add87a2c)

![365802200-cdad589a-165e-4f7b-86a4-c3aee2e52eff](https://github.com/user-attachments/assets/3b5c583d-1258-4186-8f52-2b1a38252dff)

## Result :
Thus, Bayesian Inference was successfully determined using Variable Elimination Method

