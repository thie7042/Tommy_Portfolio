# Project portfolio
This is a brief catalogue outlining my previous and ongoing research projects. For more information, feel free to reach out to me directly at thie7042@uni.sydney.edu.au, or message me on [Linkedin](https://www.linkedin.com/in/tommy-hielscher-4a40771b6/).


# Machine Learning Digital Twin for Structural Health Monitoring

![](/Images/Video_Demo.gif)


## Project brief
The novel digital twin solution that has been designed and prototyped within this research project aims to demonstrate a holistic, end-to-end fibre optic structural health monitoring strategy that integrates embedded Fibre Bragg Grating sensors, open-source software and fundamental machine learning modelling techniques. Through a collaborative partnership between Laing O’Rourke and The University of Sydney, a series of 64 fibre optic sensors and 8 temperature sensors have been embedded internally within a footbridge located in the Engineering and Technology Precinct (ETP) to continuously measure and collect structural data. These datasets have been leveraged to train a series of machine learning models and develop an integrated digital twin prototype as a collective monitoring solution.

![](/Images/ETP_Bridge.PNG)

<div align="center"> The ETP footbridge, Sydney University
</div>

## Problem statement 
Public and private authorities that manage large infrastructure projects have a responsibility and vested interest in maintaining the longevity of their assets. The structural health monitoring (SHM) methodologies which are applied to these projects conventionally prioritise minimal service disruption, efficient resource allocation and a reduction in the degree of operational risk. The value provided by effective structural health monitoring systems cannot be overstated. In the United States, there are 625,000 bridges listed by the Department of Transportation, 30 percent of which have been officially classified as structurally deficient or functionally obsolete. Furthermore, a 2001 BRIME report concluded that across three different European countries (France, Germany and the UK), deficiencies within highway bridges were present at rates of 39%, 30% and 37% respectively. 

![](/Images/Global_SHM_Stats.PNG)

Traditional techniques of non-destructive evaluation (NDE) for the monitoring of these assets have also been severely limited to routine visual examinations which are unable to provide continuous information into the long-term behaviour of these structures. A technical report published by the U.S Federal Highway administration concluded that 58% of sample average condition ratings for tested structural elements were assigned incorrectly.  These inaccurate evaluation techniques result in economically impractical maintenance schedules and uninformed resource allocation for asset management at an industry scale. The accumulative effects of stagnant industry practices and mass structural deterioration pose a significant risk to the built environment, with the potential to produce a marked decline in serviceability over time.

## Data collection
During the construction of the footbridge, six FBG strain arrays containing 16 sensors at 1.0 m spacing were installed with a spatial resolution of 6.2 mm and a strain resolution of 2 µε. These arrays were fixed to the longitudinal rebar at the bottom and top portions of the concrete slab. Additional arrays were attached along the top surface of the post-tensioning duct as an intermediary reference to evaluate the accuracy of the recorded data. Temperature sensor arrays containing 4 sensors at 5.0 m spacing were also embedded within the footbridge along the top and bottom longitudinal rebar to account for the effects of thermal variation. The installed sensors were linked to a secure interrogator system located on site, with transmitted signals periodically set at 10 second increments to simplify the data architecture and workflow used in this prototype. This signal rate was modified to 1 second increments during the loading experiment to increase the resolution of the structural analysis, before being returned to a 10 second acquisition rate for sustainable long-term data collection & monitoring. 

![](/Images/Sensor_Installation.png)

<div align="center"> Sensor installation at ETP during construction
</div>
## Tested Models
Within the scope of this research project, four machine learning models were analysed: linear regression, ridge regression, lasso regression and an artificial neural network (ANN). These techniques provided a broad spectrum of complexity and hyperparameter diversity, allowing for the identification of a suitable machine learning model that best describes the temperature-strain relationship. For the selection of suitable hyperparameters, 10-fold CV & exhaustive grid-search were used. Hyperparameters which yielded the smallest model error were retained, allowing for the performance of optimised machine learning models to be directly compared against one another.

![](/Images/Hypertune.png)

## Neural Network
Across all of the tested statistical metrics (Gaussian distribution of errors, mean absolute error (MAE), mean squared error (MSE), root mean squared error (RMSE) and the coefficient of determination), the artificial neural network generated the most robust and consistent baseline strain datasets, allowing the digital twin to accurately visualise the footbridges structural response to loading. This analysis includes the derived strain, bending moment and deflection induced within the footbridge when subject to mechanical loading events. The implementation of an artificial neural network has been modelled to forecast baseline strain behaviour as influenced by temperature variance, captured from embedded strain and temperature sensors.

![](/Images/ANN.png)

<div align="center"> ANN strain prediction
</div>

![](/Images/Norm.png)

<div align="center"> Gaussian error distribution
</div>

![](/Images/Stats.png)
<div align="center"> Statistical model comparison
</div>

## Digital Twin UI
In order to mobilise the adoption of FOS sensor technology within the structural health monitoring industry, this framework was designed as an intuitive, user friendly and insightful tool that can be integrated within the workflow of site engineers, asset inspectors and project managers. The Unity Digital twin prototype was programmed with the objective of communicating significant quantities of Big data to provide actionable insights into the structural response of an asset under load, including the induced strain, bending moment and deflection. 

![](/Images/Unity_UI.png)


# Bayesian Optimization with Gaussian Process 

## Context: Locating the maxima

![](/Images/Target_Function.png)


## Context: Building the covariance matrix

![](/Images/Covariance.png)

## Context: Sampling the Prior

![](/Images/Prior_sampling.png)

## Context: Creating the surrogate model

![](/Images/Proxy_model.png)

## Context: Optimizing the acquisition function

![](/Images/Steps.png)

* Current research: Applying Bayesian Optimization with GP to create a proxy model of computationally expensive Finite Element simulations.
* See "Master" branch for development works. This project is currently in progress, with updates to come in the following months.


## Bayesian Optimization for structural Design

Parametric Master File:
```python
# Save by TommyHielscher on 2022_04_12-13.19.16; build 2021 2020_03_07-01.50.37 167380
from part import *
from material import *
from section import *
from assembly import *
from step import *
from interaction import *
from load import *
from mesh import *
from optimization import *
from job import *
from sketch import *
from visualization import *
from connectorBehavior import *


session.journalOptions.setValues(replayGeometry=COORDINATE, recoverGeometry=COORDINATE)

# ====================== Define parameters ====================== 
T_width = 300



# ====================== Create Model ====================== 
#mdb.saveAs(pathName='C:/Users/TommyHielscher/Desktop/Abaqus_scripting/ReinforcedTBeam/TBeam.cae')

mdb.Model(modelType=STANDARD_EXPLICIT, name='TBEAM')


# ====================== Define Cross section ====================== 

mdb.models['TBEAM'].ConstrainedSketch(name='__profile__', sheetSize=2000.0)
# mdb.models['TBEAM'].sketches['__profile__'].Line(point1=(0.0, 0.0), point2=(
  #  0.0, 300.0))
# mdb.models['TBEAM'].sketches['__profile__'].geometry.findAt((0.0, 150.0))
# mdb.models['TBEAM'].sketches['__profile__'].VerticalConstraint(addUndoState=
    # False, entity=mdb.models['TBEAM'].sketches['__profile__'].geometry.findAt((
    # 0.0, 150.0), ))
# mdb.models['TBEAM'].sketches['__profile__'].undo()
mdb.models['TBEAM'].sketches['__profile__'].Line(point1=(0.0, 0.0), point2=(
    300.0, 0.0))
mdb.models['TBEAM'].sketches['__profile__'].geometry.findAt((150.0, 0.0))
mdb.models['TBEAM'].sketches['__profile__'].HorizontalConstraint(addUndoState=
    False, entity=mdb.models['TBEAM'].sketches['__profile__'].geometry.findAt((
    150.0, 0.0), ))
    
mdb.models['TBEAM'].sketches['__profile__'].Line(point1=(300.0, 0.0), point2=(
    300.0, 500.0))
mdb.models['TBEAM'].sketches['__profile__'].geometry.findAt((300.0, 250.0))
mdb.models['TBEAM'].sketches['__profile__'].VerticalConstraint(addUndoState=
    False, entity=mdb.models['TBEAM'].sketches['__profile__'].geometry.findAt((
    300.0, 250.0), ))
mdb.models['TBEAM'].sketches['__profile__'].geometry.findAt((150.0, 0.0))
mdb.models['TBEAM'].sketches['__profile__'].geometry.findAt((300.0, 250.0))
mdb.models['TBEAM'].sketches['__profile__'].PerpendicularConstraint(
    addUndoState=False, entity1=
    mdb.models['TBEAM'].sketches['__profile__'].geometry.findAt((150.0, 0.0), )
    , entity2=mdb.models['TBEAM'].sketches['__profile__'].geometry.findAt((
    300.0, 250.0), ))
mdb.models['TBEAM'].sketches['__profile__'].Line(point1=(300.0, 500.0), point2=
    (650.0, 500.0))
mdb.models['TBEAM'].sketches['__profile__'].geometry.findAt((475.0, 500.0))
mdb.models['TBEAM'].sketches['__profile__'].HorizontalConstraint(addUndoState=
    False, entity=mdb.models['TBEAM'].sketches['__profile__'].geometry.findAt((
    475.0, 500.0), ))
mdb.models['TBEAM'].sketches['__profile__'].geometry.findAt((300.0, 250.0))
mdb.models['TBEAM'].sketches['__profile__'].geometry.findAt((475.0, 500.0))
mdb.models['TBEAM'].sketches['__profile__'].PerpendicularConstraint(
    addUndoState=False, entity1=
    mdb.models['TBEAM'].sketches['__profile__'].geometry.findAt((300.0, 250.0), 
    ), entity2=mdb.models['TBEAM'].sketches['__profile__'].geometry.findAt((
    475.0, 500.0), ))
mdb.models['TBEAM'].sketches['__profile__'].Line(point1=(650.0, 500.0), point2=
    (650.0, 650.0))
mdb.models['TBEAM'].sketches['__profile__'].geometry.findAt((650.0, 575.0))
mdb.models['TBEAM'].sketches['__profile__'].VerticalConstraint(addUndoState=
    False, entity=mdb.models['TBEAM'].sketches['__profile__'].geometry.findAt((
    650.0, 575.0), ))
mdb.models['TBEAM'].sketches['__profile__'].geometry.findAt((475.0, 500.0))
mdb.models['TBEAM'].sketches['__profile__'].geometry.findAt((650.0, 575.0))
mdb.models['TBEAM'].sketches['__profile__'].PerpendicularConstraint(
    addUndoState=False, entity1=
    mdb.models['TBEAM'].sketches['__profile__'].geometry.findAt((475.0, 500.0), 
    ), entity2=mdb.models['TBEAM'].sketches['__profile__'].geometry.findAt((
    650.0, 575.0), ))
mdb.models['TBEAM'].sketches['__profile__'].Line(point1=(650.0, 650.0), point2=
    (-350.0, 650.0))
mdb.models['TBEAM'].sketches['__profile__'].geometry.findAt((150.0, 650.0))
mdb.models['TBEAM'].sketches['__profile__'].HorizontalConstraint(addUndoState=
    False, entity=mdb.models['TBEAM'].sketches['__profile__'].geometry.findAt((
    150.0, 650.0), ))
mdb.models['TBEAM'].sketches['__profile__'].geometry.findAt((650.0, 575.0))
mdb.models['TBEAM'].sketches['__profile__'].geometry.findAt((150.0, 650.0))
mdb.models['TBEAM'].sketches['__profile__'].PerpendicularConstraint(
    addUndoState=False, entity1=
    mdb.models['TBEAM'].sketches['__profile__'].geometry.findAt((650.0, 575.0), 
    ), entity2=mdb.models['TBEAM'].sketches['__profile__'].geometry.findAt((
    150.0, 650.0), ))
mdb.models['TBEAM'].sketches['__profile__'].Line(point1=(-350.0, 650.0), 
    point2=(-350.0, 500.0))
mdb.models['TBEAM'].sketches['__profile__'].geometry.findAt((-350.0, 575.0))
mdb.models['TBEAM'].sketches['__profile__'].VerticalConstraint(addUndoState=
    False, entity=mdb.models['TBEAM'].sketches['__profile__'].geometry.findAt((
    -350.0, 575.0), ))
mdb.models['TBEAM'].sketches['__profile__'].geometry.findAt((150.0, 650.0))
mdb.models['TBEAM'].sketches['__profile__'].geometry.findAt((-350.0, 575.0))
mdb.models['TBEAM'].sketches['__profile__'].PerpendicularConstraint(
    addUndoState=False, entity1=
    mdb.models['TBEAM'].sketches['__profile__'].geometry.findAt((150.0, 650.0), 
    ), entity2=mdb.models['TBEAM'].sketches['__profile__'].geometry.findAt((
    -350.0, 575.0), ))
mdb.models['TBEAM'].sketches['__profile__'].Line(point1=(-350.0, 500.0), 
    point2=(0.0, 500.0))
mdb.models['TBEAM'].sketches['__profile__'].geometry.findAt((-175.0, 500.0))
mdb.models['TBEAM'].sketches['__profile__'].HorizontalConstraint(addUndoState=
    False, entity=mdb.models['TBEAM'].sketches['__profile__'].geometry.findAt((
    -175.0, 500.0), ))
mdb.models['TBEAM'].sketches['__profile__'].geometry.findAt((-350.0, 575.0))
mdb.models['TBEAM'].sketches['__profile__'].geometry.findAt((-175.0, 500.0))
mdb.models['TBEAM'].sketches['__profile__'].PerpendicularConstraint(
    addUndoState=False, entity1=
    mdb.models['TBEAM'].sketches['__profile__'].geometry.findAt((-350.0, 
    575.0), ), entity2=
    mdb.models['TBEAM'].sketches['__profile__'].geometry.findAt((-175.0, 
    500.0), ))
mdb.models['TBEAM'].sketches['__profile__'].Line(point1=(0.0, 500.0), point2=(
    0.0, 0.0))
mdb.models['TBEAM'].sketches['__profile__'].geometry.findAt((0.0, 250.0))
mdb.models['TBEAM'].sketches['__profile__'].VerticalConstraint(addUndoState=
    False, entity=mdb.models['TBEAM'].sketches['__profile__'].geometry.findAt((
    0.0, 250.0), ))
mdb.models['TBEAM'].sketches['__profile__'].geometry.findAt((-175.0, 500.0))
mdb.models['TBEAM'].sketches['__profile__'].geometry.findAt((0.0, 250.0))
mdb.models['TBEAM'].sketches['__profile__'].PerpendicularConstraint(
    addUndoState=False, entity1=
    mdb.models['TBEAM'].sketches['__profile__'].geometry.findAt((-175.0, 
    500.0), ), entity2=
    mdb.models['TBEAM'].sketches['__profile__'].geometry.findAt((0.0, 250.0), 
    ))
mdb.models['TBEAM'].Part(dimensionality=THREE_D, name='TBEAM', type=
    DEFORMABLE_BODY)
mdb.models['TBEAM'].parts['TBEAM'].BaseSolidExtrude(depth=5000.0, sketch=
    mdb.models['TBEAM'].sketches['__profile__'])
del mdb.models['TBEAM'].sketches['__profile__']

# Save by TommyHielscher on 2022_04_12-13.27.34; build 2021 2020_03_07-01.50.37 167380

# ====================== Partitioning ====================== 

mdb.models['TBEAM'].parts['TBEAM'].PartitionCellByExtendFace(cells=
    mdb.models['TBEAM'].parts['TBEAM'].cells.findAt(((-350.0, 550.0, 
    3333.333333), )), extendFace=
    mdb.models['TBEAM'].parts['TBEAM'].faces.findAt((533.333333, 500.0, 
    3333.333333), ))
mdb.models['TBEAM'].parts['TBEAM'].DatumPlaneByOffset(flip=SIDE2, offset=200.0, 
    plane=mdb.models['TBEAM'].parts['TBEAM'].faces.findAt((200.0, 333.333333, 
    5000.0), ))
mdb.models['TBEAM'].parts['TBEAM'].DatumPlaneByOffset(flip=SIDE2, offset=200.0, 
    plane=mdb.models['TBEAM'].parts['TBEAM'].faces.findAt((100.0, 333.333333, 
    0.0), ))
mdb.models['TBEAM'].parts['TBEAM'].DatumPlaneByOffset(flip=SIDE2, offset=2500.0
    , plane=mdb.models['TBEAM'].parts['TBEAM'].faces.findAt((100.0, 333.333333, 
    0.0), ))
mdb.models['TBEAM'].parts['TBEAM'].PartitionCellByDatumPlane(cells=
    mdb.models['TBEAM'].parts['TBEAM'].cells.findAt(((200.0, 0.0, 3333.333333), 
    ), ((-116.666667, 500.0, 3333.333333), ), ), datumPlane=
    mdb.models['TBEAM'].parts['TBEAM'].datums[5])
mdb.models['TBEAM'].parts['TBEAM'].PartitionCellByDatumPlane(cells=
    mdb.models['TBEAM'].parts['TBEAM'].cells.findAt(((-233.333333, 500.0, 
    3333.333333), ), ((100.0, 0.0, 3333.333333), ), ), datumPlane=
    mdb.models['TBEAM'].parts['TBEAM'].datums[3])
    
    
# ====================== Create Longitudinal Rebar ====================== 
mdb.models['TBEAM'].parts['TBEAM'].PartitionCellByDatumPlane(cells=
    mdb.models['TBEAM'].parts['TBEAM'].cells.findAt(((533.333333, 500.0, 
    1666.666667), ), ((200.0, 0.0, 1666.666667), ), ), datumPlane=
    mdb.models['TBEAM'].parts['TBEAM'].datums[4])
mdb.models['TBEAM'].ConstrainedSketch(name='__profile__', sheetSize=2000.0)
mdb.models['TBEAM'].sketches['__profile__'].Line(point1=(0.0, 0.0), point2=(
    5000.0, 0.0))
mdb.models['TBEAM'].sketches['__profile__'].geometry.findAt((2500.0, 0.0))
mdb.models['TBEAM'].sketches['__profile__'].HorizontalConstraint(addUndoState=
    False, entity=mdb.models['TBEAM'].sketches['__profile__'].geometry.findAt((
    2500.0, 0.0), ))
mdb.models['TBEAM'].Part(dimensionality=THREE_D, name='LongBar', type=
    DEFORMABLE_BODY)
mdb.models['TBEAM'].parts['LongBar'].BaseWire(sketch=
    mdb.models['TBEAM'].sketches['__profile__'])
del mdb.models['TBEAM'].sketches['__profile__']
# Save by TommyHielscher on 2022_04_12-13.37.58; build 2021 2020_03_07-01.50.37 167380


    
# ====================== Create Stirrup ====================== 

mdb.models['TBEAM'].ConstrainedSketch(name='__profile__', sheetSize=2000.0)
mdb.models['TBEAM'].sketches['__profile__'].rectangle(point1=(25.0, 25.0), 
    point2=(275.0, 625.0))
mdb.models['TBEAM'].Part(dimensionality=THREE_D, name='STIRRUPS', type=
    DEFORMABLE_BODY)
mdb.models['TBEAM'].parts['STIRRUPS'].BaseWire(sketch=
    mdb.models['TBEAM'].sketches['__profile__'])
del mdb.models['TBEAM'].sketches['__profile__']
# Save by TommyHielscher on 2022_04_12-13.43.45; build 2021 2020_03_07-01.50.37 167380



    
# ====================== Create Transverse Bar ====================== 
mdb.models['TBEAM'].ConstrainedSketch(name='__profile__', sheetSize=2000.0)
mdb.models['TBEAM'].sketches['__profile__'].Line(point1=(0.0, 0.0), point2=(
    1000.0, 0.0))
mdb.models['TBEAM'].sketches['__profile__'].geometry.findAt((500.0, 0.0))
mdb.models['TBEAM'].sketches['__profile__'].HorizontalConstraint(addUndoState=
    False, entity=mdb.models['TBEAM'].sketches['__profile__'].geometry.findAt((
    500.0, 0.0), ))
mdb.models['TBEAM'].Part(dimensionality=THREE_D, name='TransvsBAR', type=
    DEFORMABLE_BODY)
mdb.models['TBEAM'].parts['TransvsBAR'].BaseWire(sketch=
    mdb.models['TBEAM'].sketches['__profile__'])
del mdb.models['TBEAM'].sketches['__profile__']




# ====================== Create Material Properties ====================== 
mdb.models['TBEAM'].Material(name='Steel')
mdb.models['TBEAM'].materials['Steel'].Density(table=((7.8e-09, ), ))
mdb.models['TBEAM'].materials['Steel'].Elastic(table=((210000.0, 0.3), ))
mdb.models['TBEAM'].materials['Steel'].Plastic(table=((450.0, 0.0), ))
mdb.models['TBEAM'].Material(name='Concrete')
mdb.models['TBEAM'].materials['Concrete'].Density(table=((2.4e-09, ), ))
mdb.models['TBEAM'].materials['Concrete'].Elastic(table=((15427.2973, 0.18), ))
mdb.models['TBEAM'].materials['Concrete'].ConcreteDamagedPlasticity(table=((
    35.0, 0.1, 1.16, 0.667, 0.007985), ))
mdb.models['TBEAM'].materials['Concrete'].concreteDamagedPlasticity.ConcreteCompressionHardening(
    table=((12.5, 0.0), (14.779363, 1.5e-05), (16.897181, 4e-05), (18.815096, 
    7.9e-05), (20.499689, 0.000132), (21.925443, 0.000202), (23.076855, 
    0.00029), (23.949385, 0.000396), (24.549184, 0.00052), (24.891777, 
    0.000661), (25.0, 0.000816), (24.901601, 0.000985), (24.626862, 0.001166), 
    (24.206509, 0.001356), (23.670071, 0.001553), (23.044731, 0.001756), (
    22.354643, 0.001964), (21.620626, 0.002174), (20.860155, 0.002386), (
    20.087539, 0.002598), (19.314226, 0.002811), (18.549152, 0.003023), (
    17.799119, 0.003235), (17.069142, 0.003445), (16.362775, 0.003653), (
    15.682397, 0.00386), (15.029454, 0.004065), (14.404665, 0.004268), (
    13.80819, 0.004469), (13.23977, 0.004669), (12.698832, 0.004866), (
    12.184584, 0.005062), (11.69608, 0.005257), (11.232271, 0.005449), (
    10.792054, 0.005641), (10.374298, 0.00583), (9.977867, 0.006019), (
    9.601643, 0.006206), (9.244531, 0.006392), (8.905476, 0.006576), (8.583462, 
    0.00676), (8.277519, 0.006942), (7.986728, 0.007124), (7.710212, 0.007304), 
    (7.5, 0.007448)))
mdb.models['TBEAM'].materials['Concrete'].concreteDamagedPlasticity.ConcreteTensionStiffening(
    table=((3.0, 0.0), (1.664354, 0.000281), (1.179148, 0.000507), (0.923358, 
    0.000718), (0.76383, 0.000923), (0.654173, 0.001124), (0.573836, 0.001324), 
    (0.512265, 0.001522), (0.463463, 0.00172), (0.423761, 0.001917)))
mdb.models['TBEAM'].materials['Concrete'].concreteDamagedPlasticity.ConcreteCompressionDamage(
    table=((0.0, 0.0), (0.0, 1.5e-05), (0.0, 4e-05), (0.0, 7.9e-05), (0.0, 
    0.000132), (0.0, 0.000202), (0.0, 0.00029), (0.0, 0.000396), (0.0, 
    0.00052), (0.0, 0.000661), (0.0, 0.000816), (0.003936, 0.000985), (
    0.014926, 0.001166), (0.03174, 0.001356), (0.053197, 0.001553), (0.078211, 
    0.001756), (0.105814, 0.001964), (0.135175, 0.002174), (0.165594, 
    0.002386), (0.196498, 0.002598), (0.227431, 0.002811), (0.258034, 
    0.003023), (0.288035, 0.003235), (0.317234, 0.003445), (0.345489, 
    0.003653), (0.372704, 0.00386), (0.398822, 0.004065), (0.423813, 0.004268), 
    (0.447672, 0.004469), (0.470409, 0.004669), (0.492047, 0.004866), (
    0.512617, 0.005062), (0.532157, 0.005257), (0.550709, 0.005449), (0.568318, 
    0.005641), (0.585028, 0.00583), (0.600885, 0.006019), (0.615934, 0.006206), 
    (0.630219, 0.006392), (0.643781, 0.006576), (0.656662, 0.00676), (0.668899, 
    0.006942), (0.680531, 0.007124), (0.691592, 0.007304), (0.7, 0.007448)))
mdb.models['TBEAM'].materials['Concrete'].concreteDamagedPlasticity.ConcreteTensionDamage(
    table=((0.0, 0.0), (0.445215, 0.000281), (0.606951, 0.000507), (0.692214, 
    0.000718), (0.74539, 0.000923), (0.781942, 0.001124), (0.808721, 0.001324), 
    (0.829245, 0.001522), (0.845512, 0.00172), (0.858746, 0.001917)))
mdb.models['TBEAM'].HomogeneousSolidSection(material='Concrete', name=
    'Concrete', thickness=None)
    
mdb.models['TBEAM'].TrussSection(area=50.24, material='Steel', name=
    'SteelRebar')
    
    
    
    
    
    
mdb.models['TBEAM'].parts['LongBar'].Set(edges=
    mdb.models['TBEAM'].parts['LongBar'].edges.findAt(((1250.0, 0.0, 0.0), )), 
    name='Set-1')
    
mdb.models['TBEAM'].parts['LongBar'].SectionAssignment(offset=0.0, offsetField=
    '', offsetType=MIDDLE_SURFACE, region=
    mdb.models['TBEAM'].parts['LongBar'].sets['Set-1'], sectionName=
    'SteelRebar', thicknessAssignment=FROM_SECTION)
mdb.models['TBEAM'].parts['STIRRUPS'].Set(edges=
    mdb.models['TBEAM'].parts['STIRRUPS'].edges.findAt(((212.5, 25.0, 0.0), ), 
    ((275.0, 475.0, 0.0), ), ((87.5, 625.0, 0.0), ), ((25.0, 175.0, 0.0), ), ), 
    name='Set-1')
mdb.models['TBEAM'].parts['STIRRUPS'].SectionAssignment(offset=0.0, 
    offsetField='', offsetType=MIDDLE_SURFACE, region=
    mdb.models['TBEAM'].parts['STIRRUPS'].sets['Set-1'], sectionName=
    'SteelRebar', thicknessAssignment=FROM_SECTION)
mdb.models['TBEAM'].parts['TBEAM'].Set(cells=
    mdb.models['TBEAM'].parts['TBEAM'].cells.findAt(((0.0, 166.666667, 
    133.333333), ), ((300.0, 166.666667, 966.666667), ), ((-16.666667, 650.0, 
    133.333333), ), ((200.0, 333.333333, 5000.0), ), ((300.0, 333.333333, 
    4033.333333), ), ((416.666667, 500.0, 4866.666667), ), ((-233.333333, 
    500.0, 966.666667), ), ((533.333333, 500.0, 4033.333333), ), ), name=
    'Set-1')
mdb.models['TBEAM'].parts['TBEAM'].SectionAssignment(offset=0.0, offsetField=''
    , offsetType=MIDDLE_SURFACE, region=
    mdb.models['TBEAM'].parts['TBEAM'].sets['Set-1'], sectionName='Concrete', 
    thicknessAssignment=FROM_SECTION)
mdb.models['TBEAM'].parts['TransvsBAR'].Set(edges=
    mdb.models['TBEAM'].parts['TransvsBAR'].edges.findAt(((250.0, 0.0, 0.0), ))
    , name='Set-1')
mdb.models['TBEAM'].parts['TransvsBAR'].SectionAssignment(offset=0.0, 
    offsetField='', offsetType=MIDDLE_SURFACE, region=
    mdb.models['TBEAM'].parts['TransvsBAR'].sets['Set-1'], sectionName=
    'SteelRebar', thicknessAssignment=FROM_SECTION)
    
    
mdb.models['TBEAM'].rootAssembly.DatumCsysByDefault(CARTESIAN)
mdb.models['TBEAM'].rootAssembly.Instance(dependent=ON, name='LongBar-1', part=
    mdb.models['TBEAM'].parts['LongBar'])
mdb.models['TBEAM'].rootAssembly.Instance(dependent=ON, name='STIRRUPS-1', 
    part=mdb.models['TBEAM'].parts['STIRRUPS'])
mdb.models['TBEAM'].rootAssembly.Instance(dependent=ON, name='TBEAM-1', part=
    mdb.models['TBEAM'].parts['TBEAM'])
mdb.models['TBEAM'].rootAssembly.Instance(dependent=ON, name='TransvsBAR-1', 
    part=mdb.models['TBEAM'].parts['TransvsBAR'])
    
    
    
# ====================== Translations ====================== 
mdb.models['TBEAM'].rootAssembly.instances['STIRRUPS-1'].translate(vector=(0.0, 
    0.0, 0.0))
mdb.models['TBEAM'].rootAssembly.instances['TBEAM-1'].translate(vector=(5510.0, 
    0.0, 0.0))
mdb.models['TBEAM'].rootAssembly.instances['TransvsBAR-1'].translate(vector=(
    6310.0, 0.0, 0.0))
mdb.models['TBEAM'].rootAssembly.DatumPointByOffset(point=
    mdb.models['TBEAM'].rootAssembly.instances['TBEAM-1'].vertices.findAt((
    5810.0, 0.0, 0.0), ), vector=(-25.0, 25.0, 0.0))
mdb.models['TBEAM'].rootAssembly.translate(instanceList=('STIRRUPS-1', ), 
    vector=(5510.0, 0.0, 0.0))
mdb.models['TBEAM'].rootAssembly.rotate(angle=90.0, axisDirection=(0.0, 150.0, 
    0.0), axisPoint=(5160.0, 500.0, 0.0), instanceList=('LongBar-1', ))
mdb.models['TBEAM'].rootAssembly.DatumPointByOffset(point=
    mdb.models['TBEAM'].rootAssembly.instances['TBEAM-1'].vertices.findAt((
    5810.0, 0.0, 0.0), ), vector=(-50.0, 50.0, 0.0))
mdb.models['TBEAM'].rootAssembly.translate(instanceList=('LongBar-1', ), 
    vector=(600.0, 50.0, -160.0))
    
    
# ====================== Copy to create pattern (Longitudinal Rebar) ====================== 
mdb.models['TBEAM'].rootAssembly.LinearInstancePattern(direction1=(-1.0, 0.0, 
    0.0), direction2=(0.0, 1.0, 0.0), instanceList=('LongBar-1', ), number1=3, 
    number2=2, spacing1=100.0, spacing2=500.0)

# ====================== Copy to create pattern (Stirrups) ====================== 
mdb.models['TBEAM'].rootAssembly.LinearInstancePattern(direction1=(0.0, 0.0, 
    1.0), direction2=(0.0, 1.0, 0.0), instanceList=('STIRRUPS-1', ), number1=26
    , number2=1, spacing1=200.0, spacing2=600.0)
    
    
del mdb.models['TBEAM'].rootAssembly.features['STIRRUPS-1']
del mdb.models['TBEAM'].rootAssembly.features['STIRRUPS-1-lin-26-1']


mdb.models['TBEAM'].rootAssembly.translate(instanceList=('TransvsBAR-1', ), 
    vector=(-1150.0, 625.0, 200.0))
    
    

# ====================== Copy to create pattern (Transverse bars ====================== 
mdb.models['TBEAM'].rootAssembly.LinearInstancePattern(direction1=(0.0, 0.0, 
    1.0), direction2=(0.0, 1.0, 0.0), instanceList=('TransvsBAR-1', ), number1=
    24, number2=1, spacing1=200.0, spacing2=1.0)
mdb.models['TBEAM'].rootAssembly.LinearInstancePattern(direction1=(-1.0, 0.0, 
    0.0), direction2=(0.0, 1.0, 0.0), instanceList=('LongBar-1-lin-3-2', ), 
    number1=2, number2=2, spacing1=200.0, spacing2=1.0)
    
# ====================== Copy to create pattern (additional longitudinal rebar) ====================== 
mdb.models['TBEAM'].rootAssembly.LinearInstancePattern(direction1=(1.0, 0.0, 
    0.0), direction2=(0.0, 1.0, 0.0), instanceList=('LongBar-1-lin-1-2', ), 
    number1=2, number2=2, spacing1=200.0, spacing2=1.0)
# Save by TommyHielscher on 2022_04_12-14.37.03; build 2021 2020_03_07-01.50.37 167380


# ====================== Apply Boundary Conditions (Pinned & Roller) ====================== 

mdb.models['TBEAM'].rootAssembly.Set(edges=
    mdb.models['TBEAM'].rootAssembly.instances['TBEAM-1'].edges.findAt(((
    5585.0, 0.0, 200.0), )), name='Set-1')
mdb.models['TBEAM'].DisplacementBC(amplitude=UNSET, createStepName='Initial', 
    distributionType=UNIFORM, fieldName='', localCsys=None, name='BC-1', 
    region=mdb.models['TBEAM'].rootAssembly.sets['Set-1'], u1=SET, u2=SET, u3=
    SET, ur1=UNSET, ur2=UNSET, ur3=UNSET)
mdb.models['TBEAM'].rootAssembly.Set(edges=
    mdb.models['TBEAM'].rootAssembly.instances['TBEAM-1'].edges.findAt(((
    5735.0, 0.0, 4800.0), )), name='Set-2')
mdb.models['TBEAM'].DisplacementBC(amplitude=UNSET, createStepName='Initial', 
    distributionType=UNIFORM, fieldName='', localCsys=None, name='Roller', 
    region=mdb.models['TBEAM'].rootAssembly.sets['Set-2'], u1=SET, u2=SET, u3=
    UNSET, ur1=UNSET, ur2=UNSET, ur3=UNSET)
# Save by TommyHielscher on 2022_04_12-14.50.52; build 2021 2020_03_07-01.50.37 167380


# ====================== Apply Pressure ====================== 


mdb.models['TBEAM'].StaticStep(name='Step-1', previous='Initial')
mdb.models['TBEAM'].rootAssembly.Surface(name='Surf-1', side1Faces=
    mdb.models['TBEAM'].rootAssembly.instances['TBEAM-1'].faces.findAt(((
    5826.666667, 650.0, 966.666667), ), ((5826.666667, 650.0, 4866.666667), ), 
    ((5493.333333, 650.0, 133.333333), ), ((5493.333333, 650.0, 4033.333333), 
    ), ))
mdb.models['TBEAM'].Pressure(amplitude=UNSET, createStepName='Step-1', 
    distributionType=UNIFORM, field='', magnitude=10.0e-6, name='Load-1', region=
    mdb.models['TBEAM'].rootAssembly.surfaces['Surf-1'])
# Save by TommyHielscher on 2022_04_12-14.57.21; build 2021 2020_03_07-01.50.37 167380
# Save by TommyHielscher on 2022_04_12-14.57.23; build 2021 2020_03_07-01.50.37 167380


# ====================== Select Output ====================== 


mdb.models['TBEAM'].fieldOutputRequests['F-Output-1'].setValues(variables=('S', 
    'PE', 'PEEQ', 'PEMAG', 'LE', 'U', 'RF', 'CF', 'CSTRESS', 'CDISP', 
    'DAMAGEC', 'DAMAGET'))
    

# ====================== Set constraints (embedded region) ====================== 


mdb.models['TBEAM'].rootAssembly.Set(edges=
    mdb.models['TBEAM'].rootAssembly.instances['LongBar-1'].edges.findAt(((
    5760.0, 50.0, 3750.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['TransvsBAR-1'].edges.findAt(((
    5410.0, 625.0, 200.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['LongBar-1-lin-1-2'].edges.findAt(
    ((5760.0, 550.0, 3750.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['LongBar-1-lin-2-1'].edges.findAt(
    ((5660.0, 50.0, 3750.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['LongBar-1-lin-2-2'].edges.findAt(
    ((5660.0, 550.0, 3750.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['LongBar-1-lin-3-1'].edges.findAt(
    ((5560.0, 50.0, 3750.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['LongBar-1-lin-3-2'].edges.findAt(
    ((5560.0, 550.0, 3750.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['STIRRUPS-1-lin-2-1'].edges.findAt(
    ((5722.5, 25.0, 200.0), ), ((5785.0, 475.0, 200.0), ), ((5597.5, 625.0, 
    200.0), ), ((5535.0, 175.0, 200.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['STIRRUPS-1-lin-3-1'].edges.findAt(
    ((5722.5, 25.0, 400.0), ), ((5785.0, 475.0, 400.0), ), ((5597.5, 625.0, 
    400.0), ), ((5535.0, 175.0, 400.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['STIRRUPS-1-lin-4-1'].edges.findAt(
    ((5722.5, 25.0, 600.0), ), ((5785.0, 475.0, 600.0), ), ((5597.5, 625.0, 
    600.0), ), ((5535.0, 175.0, 600.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['STIRRUPS-1-lin-5-1'].edges.findAt(
    ((5722.5, 25.0, 800.0), ), ((5785.0, 475.0, 800.0), ), ((5597.5, 625.0, 
    800.0), ), ((5535.0, 175.0, 800.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['STIRRUPS-1-lin-6-1'].edges.findAt(
    ((5722.5, 25.0, 1000.0), ), ((5785.0, 475.0, 1000.0), ), ((5597.5, 625.0, 
    1000.0), ), ((5535.0, 175.0, 1000.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['STIRRUPS-1-lin-7-1'].edges.findAt(
    ((5722.5, 25.0, 1200.0), ), ((5785.0, 475.0, 1200.0), ), ((5597.5, 625.0, 
    1200.0), ), ((5535.0, 175.0, 1200.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['STIRRUPS-1-lin-8-1'].edges.findAt(
    ((5722.5, 25.0, 1400.0), ), ((5785.0, 475.0, 1400.0), ), ((5597.5, 625.0, 
    1400.0), ), ((5535.0, 175.0, 1400.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['STIRRUPS-1-lin-9-1'].edges.findAt(
    ((5722.5, 25.0, 1600.0), ), ((5785.0, 475.0, 1600.0), ), ((5597.5, 625.0, 
    1600.0), ), ((5535.0, 175.0, 1600.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['STIRRUPS-1-lin-10-1'].edges.findAt(
    ((5722.5, 25.0, 1800.0), ), ((5785.0, 475.0, 1800.0), ), ((5597.5, 625.0, 
    1800.0), ), ((5535.0, 175.0, 1800.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['STIRRUPS-1-lin-11-1'].edges.findAt(
    ((5722.5, 25.0, 2000.0), ), ((5785.0, 475.0, 2000.0), ), ((5597.5, 625.0, 
    2000.0), ), ((5535.0, 175.0, 2000.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['STIRRUPS-1-lin-12-1'].edges.findAt(
    ((5722.5, 25.0, 2200.0), ), ((5785.0, 475.0, 2200.0), ), ((5597.5, 625.0, 
    2200.0), ), ((5535.0, 175.0, 2200.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['STIRRUPS-1-lin-13-1'].edges.findAt(
    ((5722.5, 25.0, 2400.0), ), ((5785.0, 475.0, 2400.0), ), ((5597.5, 625.0, 
    2400.0), ), ((5535.0, 175.0, 2400.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['STIRRUPS-1-lin-14-1'].edges.findAt(
    ((5722.5, 25.0, 2600.0), ), ((5785.0, 475.0, 2600.0), ), ((5597.5, 625.0, 
    2600.0), ), ((5535.0, 175.0, 2600.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['STIRRUPS-1-lin-15-1'].edges.findAt(
    ((5722.5, 25.0, 2800.0), ), ((5785.0, 475.0, 2800.0), ), ((5597.5, 625.0, 
    2800.0), ), ((5535.0, 175.0, 2800.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['STIRRUPS-1-lin-16-1'].edges.findAt(
    ((5722.5, 25.0, 3000.0), ), ((5785.0, 475.0, 3000.0), ), ((5597.5, 625.0, 
    3000.0), ), ((5535.0, 175.0, 3000.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['STIRRUPS-1-lin-17-1'].edges.findAt(
    ((5722.5, 25.0, 3200.0), ), ((5785.0, 475.0, 3200.0), ), ((5597.5, 625.0, 
    3200.0), ), ((5535.0, 175.0, 3200.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['STIRRUPS-1-lin-18-1'].edges.findAt(
    ((5722.5, 25.0, 3400.0), ), ((5785.0, 475.0, 3400.0), ), ((5597.5, 625.0, 
    3400.0), ), ((5535.0, 175.0, 3400.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['STIRRUPS-1-lin-19-1'].edges.findAt(
    ((5722.5, 25.0, 3600.0), ), ((5785.0, 475.0, 3600.0), ), ((5597.5, 625.0, 
    3600.0), ), ((5535.0, 175.0, 3600.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['STIRRUPS-1-lin-20-1'].edges.findAt(
    ((5722.5, 25.0, 3800.0), ), ((5785.0, 475.0, 3800.0), ), ((5597.5, 625.0, 
    3800.0), ), ((5535.0, 175.0, 3800.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['STIRRUPS-1-lin-21-1'].edges.findAt(
    ((5722.5, 25.0, 4000.0), ), ((5785.0, 475.0, 4000.0), ), ((5597.5, 625.0, 
    4000.0), ), ((5535.0, 175.0, 4000.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['STIRRUPS-1-lin-22-1'].edges.findAt(
    ((5722.5, 25.0, 4200.0), ), ((5785.0, 475.0, 4200.0), ), ((5597.5, 625.0, 
    4200.0), ), ((5535.0, 175.0, 4200.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['STIRRUPS-1-lin-23-1'].edges.findAt(
    ((5722.5, 25.0, 4400.0), ), ((5785.0, 475.0, 4400.0), ), ((5597.5, 625.0, 
    4400.0), ), ((5535.0, 175.0, 4400.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['STIRRUPS-1-lin-24-1'].edges.findAt(
    ((5722.5, 25.0, 4600.0), ), ((5785.0, 475.0, 4600.0), ), ((5597.5, 625.0, 
    4600.0), ), ((5535.0, 175.0, 4600.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['STIRRUPS-1-lin-25-1'].edges.findAt(
    ((5722.5, 25.0, 4800.0), ), ((5785.0, 475.0, 4800.0), ), ((5597.5, 625.0, 
    4800.0), ), ((5535.0, 175.0, 4800.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['TransvsBAR-1-lin-2-1'].edges.findAt(
    ((5410.0, 625.0, 400.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['TransvsBAR-1-lin-3-1'].edges.findAt(
    ((5410.0, 625.0, 600.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['TransvsBAR-1-lin-4-1'].edges.findAt(
    ((5410.0, 625.0, 800.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['TransvsBAR-1-lin-5-1'].edges.findAt(
    ((5410.0, 625.0, 1000.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['TransvsBAR-1-lin-6-1'].edges.findAt(
    ((5410.0, 625.0, 1200.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['TransvsBAR-1-lin-7-1'].edges.findAt(
    ((5410.0, 625.0, 1400.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['TransvsBAR-1-lin-8-1'].edges.findAt(
    ((5410.0, 625.0, 1600.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['TransvsBAR-1-lin-9-1'].edges.findAt(
    ((5410.0, 625.0, 1800.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['TransvsBAR-1-lin-10-1'].edges.findAt(
    ((5410.0, 625.0, 2000.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['TransvsBAR-1-lin-11-1'].edges.findAt(
    ((5410.0, 625.0, 2200.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['TransvsBAR-1-lin-12-1'].edges.findAt(
    ((5410.0, 625.0, 2400.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['TransvsBAR-1-lin-13-1'].edges.findAt(
    ((5410.0, 625.0, 2600.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['TransvsBAR-1-lin-14-1'].edges.findAt(
    ((5410.0, 625.0, 2800.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['TransvsBAR-1-lin-15-1'].edges.findAt(
    ((5410.0, 625.0, 3000.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['TransvsBAR-1-lin-16-1'].edges.findAt(
    ((5410.0, 625.0, 3200.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['TransvsBAR-1-lin-17-1'].edges.findAt(
    ((5410.0, 625.0, 3400.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['TransvsBAR-1-lin-18-1'].edges.findAt(
    ((5410.0, 625.0, 3600.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['TransvsBAR-1-lin-19-1'].edges.findAt(
    ((5410.0, 625.0, 3800.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['TransvsBAR-1-lin-20-1'].edges.findAt(
    ((5410.0, 625.0, 4000.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['TransvsBAR-1-lin-21-1'].edges.findAt(
    ((5410.0, 625.0, 4200.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['TransvsBAR-1-lin-22-1'].edges.findAt(
    ((5410.0, 625.0, 4400.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['TransvsBAR-1-lin-23-1'].edges.findAt(
    ((5410.0, 625.0, 4600.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['TransvsBAR-1-lin-24-1'].edges.findAt(
    ((5410.0, 625.0, 4800.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['LongBar-1-lin-3-2-lin-1-2'].edges.findAt(
    ((5560.0, 551.0, 3750.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['LongBar-1-lin-3-2-lin-2-1'].edges.findAt(
    ((5360.0, 550.0, 3750.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['LongBar-1-lin-3-2-lin-2-2'].edges.findAt(
    ((5360.0, 551.0, 3750.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['LongBar-1-lin-1-2-lin-1-2'].edges.findAt(
    ((5760.0, 551.0, 3750.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['LongBar-1-lin-1-2-lin-2-1'].edges.findAt(
    ((5960.0, 550.0, 3750.0), ), )+\
    mdb.models['TBEAM'].rootAssembly.instances['LongBar-1-lin-1-2-lin-2-2'].edges.findAt(
    ((5960.0, 551.0, 3750.0), ), ), name='m_Set-3')
mdb.models['TBEAM'].rootAssembly.Set(cells=
    mdb.models['TBEAM'].rootAssembly.instances['TBEAM-1'].cells.findAt(((
    5510.0, 166.666667, 133.333333), ), ((5810.0, 166.666667, 966.666667), ), (
    (5493.333333, 650.0, 133.333333), ), ((5710.0, 333.333333, 5000.0), ), ((
    5810.0, 333.333333, 4033.333333), ), ((5926.666667, 500.0, 4866.666667), ), 
    ((5276.666667, 500.0, 966.666667), ), ((6043.333333, 500.0, 4033.333333), 
    ), ), name='s_Set-3')
mdb.models['TBEAM'].EmbeddedRegion(absoluteTolerance=0.0, embeddedRegion=
    mdb.models['TBEAM'].rootAssembly.sets['m_Set-3'], fractionalTolerance=0.05, 
    hostRegion=mdb.models['TBEAM'].rootAssembly.sets['s_Set-3'], name=
    'Constraint-1', toleranceMethod=BOTH, weightFactorTolerance=1e-06)
# Save by TommyHielscher on 2022_04_12-15.03.51; build 2021 2020_03_07-01.50.37 167380


# ====================== Create Mesh ====================== 

mdb.models['TBEAM'].parts['LongBar'].seedPart(deviationFactor=0.1, 
    minSizeFactor=0.1, size=50.0)
mdb.models['TBEAM'].parts['LongBar'].generateMesh()
mdb.models['TBEAM'].parts['STIRRUPS'].seedPart(deviationFactor=0.1, 
    minSizeFactor=0.1, size=50.0)
mdb.models['TBEAM'].parts['STIRRUPS'].generateMesh()
mdb.models['TBEAM'].parts['TBEAM'].seedPart(deviationFactor=0.1, minSizeFactor=
    0.1, size=25.0)
mdb.models['TBEAM'].parts['TBEAM'].generateMesh()
mdb.models['TBEAM'].parts['TransvsBAR'].seedPart(deviationFactor=0.1, 
    minSizeFactor=0.1, size=50.0)
mdb.models['TBEAM'].parts['TransvsBAR'].generateMesh()
# Save by TommyHielscher on 2022_04_12-15.11.59; build 2021 2020_03_07-01.50.37 167380



# ====================== Set Element Type ====================== 

mdb.models['TBEAM'].parts['TransvsBAR'].setElementType(elemTypes=(ElemType(
    elemCode=T3D2, elemLibrary=STANDARD), ), regions=(
    mdb.models['TBEAM'].parts['TransvsBAR'].edges.findAt(((250.0, 0.0, 0.0), 
    )), ))
mdb.models['TBEAM'].parts['LongBar'].setElementType(elemTypes=(ElemType(
    elemCode=T3D2, elemLibrary=STANDARD), ), regions=(
    mdb.models['TBEAM'].parts['LongBar'].edges.findAt(((1250.0, 0.0, 0.0), )), 
    ))
mdb.models['TBEAM'].parts['STIRRUPS'].setElementType(elemTypes=(ElemType(
    elemCode=T3D2, elemLibrary=STANDARD), ), regions=(
    mdb.models['TBEAM'].parts['STIRRUPS'].edges.findAt(((212.5, 25.0, 0.0), ), 
    ((275.0, 475.0, 0.0), ), ((87.5, 625.0, 0.0), ), ((25.0, 175.0, 0.0), ), ), 
    ))
mdb.models['TBEAM'].parts['TBEAM'].setElementType(elemTypes=(ElemType(
    elemCode=C3D8R, elemLibrary=STANDARD, secondOrderAccuracy=OFF, 
    kinematicSplit=AVERAGE_STRAIN, hourglassControl=DEFAULT, 
    distortionControl=DEFAULT), ElemType(elemCode=C3D6, elemLibrary=STANDARD), 
    ElemType(elemCode=C3D4, elemLibrary=STANDARD)), regions=(
    mdb.models['TBEAM'].parts['TBEAM'].cells.findAt(((0.0, 166.666667, 
    133.333333), ), ((300.0, 166.666667, 966.666667), ), ((-16.666667, 650.0, 
    133.333333), ), ((200.0, 333.333333, 5000.0), ), ((300.0, 333.333333, 
    4033.333333), ), ((416.666667, 500.0, 4866.666667), ), ((-233.333333, 
    500.0, 966.666667), ), ((533.333333, 500.0, 4033.333333), ), ), ))
# Save by TommyHielscher on 2022_04_12-15.21.43; build 2021 2020_03_07-01.50.37 167380



# ====================== Create Job ====================== 

mdb.Job(atTime=None, contactPrint=OFF, description='', echoPrint=OFF, 
    explicitPrecision=SINGLE, getMemoryFromAnalysis=True, historyPrint=OFF, 
    memory=90, memoryUnits=PERCENTAGE, model='TBEAM', modelPrint=OFF, 
    multiprocessingMode=DEFAULT, name='TBEAM', nodalOutputPrecision=SINGLE, 
    numCpus=4, numDomains=4, numGPUs=0, queue=None, resultsFormat=ODB, scratch=
    '', type=ANALYSIS, userSubroutine='', waitHours=0, waitMinutes=0)
# Save by TommyHielscher on 2022_04_12-15.08.22; build 2021 2020_03_07-01.50.37 167380


# ====================== Submit Job ====================== 

#mdb.models['TBEAM'].rootAssembly.regenerate()
mdb.jobs['TBEAM'].submit(consistencyChecking=OFF)
```
