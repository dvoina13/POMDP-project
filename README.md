# POMDP-project

cells 1 - 3: import libraries, get data etc.

cell 4: compute firing rates for different sizes and orientations of mushrooms and birds. Parameters model a  hill function  that determines uncertainty (the more distant sizes and orientations are from the trained ones, the more uncertan the mouse is). Parameters can be initially taken from the accumulator model fits. 

cell 5: simple inferences from the data

cell 6: simulation of the decision process. Subjects start at a certain distance from the target, set by the parameter
distance_left_original. The target object is taken from the empirical data - i.e. identity, size, orientation from 
actual experiments. With each time step (time is sampled from an exponential distribution that depends on the firing rates),
the subject gathers evidence for mushroom/bird (m_R, m_L, sometimes referred to in the code as left/right objects). The belief
pdf is updated every time step (belief_pdf), which measures how much probability we assign to the parameter mu (see notation in
paper). The closer mu is to 1 or 0 the more certain we are of the identity of the object; the closer it is to 0.5 the more
uncertain we are. Value and policy are updated each trial. These are a function of belief states, a belief state being 
(m_R, m_L, dist) - so a function of how much evidence is gathered + how close we are to the target.

This function is extremely long and probably very hard to understand. The goal here is to break it down in smaller pieces that
are more easily understandable. I have went through the code line by line this week and haven't found errors, but I think 
something is going wrong because of results from cell 10.

cell 7: RUN this CELL to RUN the SIMULATION. Set perceptual parameters and distance to target.

cell 8: Look at value and policy learned. 1 for value and -1 for policy denote states that haven't been reached so just 
ignore those.

cell 9: Accuracy, % actions 1 taken and other variables that show the characteristics of the simulation. There are 3 possible
actions: 0,1,2 that correspond to velocities. Velocity (or action) 0 means stop, velocity 1 and 2 are going slower vs. faster 
respectively. When the target thinks it's far away from the target the only possible actions are 1 and 2 (simplifying
assumption), when it thinks it reached the target it can choose 0,1,2.

cell 10: There are 2 predictions that the model needs to make and we test the first one here. Increasing uncertainty should
decrease accuracy and increase % of trials where velocity = 1 (as opposed to 2). The reasoning is that the subjects slow 
down to gather more evidence.

I forgot to label the axes for the 3 figures at the end of the cell output here (takes long to run this cell):

figure (1): uncertainty vs. % trials with velocity = 1

figure (2): uncertainty vs. % trials with velocity = 1 in the last 10% of the trials

figure (3): uncertainty vs. accuracy

These results are not what I expected so there is probably something wrong going on in the simulation. Accuracy should 
decrease as uncertainty increases.

cell 11: Second prediction of the model: as distance to target increases, accuracy increases and % trials with velocity = 1
decreases (as opposed to instances with velocity =2).

figure (1): distance vs. %trials with velocity  =1

figure (2): distance vs. %trials with velocity  =1, last 10% trials

figure (3): distance to target vs. accuracy

Thisis what we expect.

