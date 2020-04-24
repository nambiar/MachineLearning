# QLearningAgents Python File

### QLearningAgent

The class which computes the QLearning init , update and calculate the Qstate parameters

This class inherits an abstract base class called ReinforcementAgent

#### ______init______

when the __init_ is called from the QLearningAgent class it just inherits the following values  from base class 

ReinforcementAgent.

        self.episodesSoFar = 0
        self.accumTrainRewards = 0.0
        self.accumTestRewards = 0.0
        self.numTraining = int(numTraining)
        self.epsilon = float(epsilon)
        self.alpha = float(alpha)
        self.discount = float(gamma)
`self.qValues = util.Counter()`

A variable *qValues* to add state and action

#### getQValue

A helper functions which returns the stored node Q(state,for specific action) and if that state is not present 0.

#### getLegalActions

A function which has all the actions that a given state can do 

getLegalActions(For the first box of the pacman(bottom left)) = {SIDE, UP}

#### computeValueFromQValues

The second term in the temporal equation " Maximum expected future reward "

![](https://miro.medium.com/max/1400/1*EQ-tDj-iMdsHlGKUR81Xgw.png))

This function calculates that

- [ ] Get the legal actions for the state
- [ ] Calculate the individual Q values for the actions
- [ ] Return max value from them

#### computeActionFromQValues

From the above mentioned image, After calculating the Q values this function determines the action which needs to be taken for a given state

- [ ] Get the legal actions for the state
- [ ] Calculate the individual Q values for the actions
- [ ] Return the action which has the max value

#### getAction

Compute the action to be done in this state using the above mentioned functions

- greedy strategy /stochastic introduced using epsilon using flipCoin with epsilon 
- The random.choice is the exploration in the Agent 
- getPolicy is actually calling computing action from Q value which is the action with biggest reward.

#### Update

![](<https://miro.medium.com/max/1400/1*EQ-tDj-iMdsHlGKUR81Xgw.png>)

This calculates the Q(s,a) update

alphadiff = Learning Rate *( Reward  + DiscountRate * (Max Expected future reward)  - Current Q value)

The next part is the gradient ascent  wherein you add the diff to the weights





