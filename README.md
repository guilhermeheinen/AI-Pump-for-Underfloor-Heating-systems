# AI pump

This code have been programmed by Christian Blad, Sajuran and Søren Koch aka. Group VT4103A
The reinforcement learning framework is based on the original code from udemy course https://www.udemy.com/artificial-intelligence-az/
From Aalborg University
The program controls a pump from Grundfos A/S in a underfloor heating system where room(s) depending on environment
needs to be a certain reference room temperature where the temperature running through the pipes
under the floor is regulated and valve to the different circuits is open/closed depending on environment
  
# The following libraries are needed to run
* tensorflow or pytorch
* numpy
* matplotlib
  
# Optional arguments to run on main.py:  
    -swe    -- (Start Weights and Experience) - Name of Weights to start with, from saves/weigts')
    -ewe    -- (End Weights and Experience) - Name of Weights which is saved in saves/weights and name of brain plot which is saved in saves/plots (default is <default_name>)')
    -ers    -- (experience replay sample size) - how much to sample when learning, Note: only for tf_dqnet (160 is default)')
    -erb    -- (experience replaybatch size) - how much to use when learning (default 300)')
    -erc    -- (experience replay capacity) - size of experience replay memory (default 100000)')
    -lr'    -- (Learning rate) - (0.001 is default')
    -gamma  -- (Discount factor) - (0.9 is default')
    -tau    -- (Temperature) - For Softmax function, note: when choosing torch_dqnet tau should be 1-10 (50 is default')
    -es     -- (Epsilon start) - For epsilon Greedy start value, meaning random action is taken 90%% of the time (0.9 is default)')
    -ee     -- (Epsilon end) - For epsilon Greedy end value, meaning random action is taken 5%% of the time after decay(0.05 is default)')
    -ed     -- (Epsilon decay) - For epsilon Greedy, by default decay from 0.9 to 0.1 over 2000 steps (2000 is default')
    -acs    -- (action selector) - (softmax is default) Note: epsilon greedy is not made for eligibility trace', choices=[SOFTMAX, EPS])
    -en     -- (eligibility trace steps n) - How many steps should eligiblity trace take (1 is default, is simple one step Q learning)')
    -hn     -- (hidden neurons) - For Q-network (60 is default for hidden layers')
    -hl     -- (hidden layer(s)) - For Q-network (1 is default)', choices=[ONE, TWO])
    -t1     -- Reference temperature in circuit 1 regarding reward policy, go to simulink model if another reference temperature is rewarding regarding speed control (default 22)')
    -t2     -- Reference temperature in circuit 2 regarding reward policy, go to simulink model if another reference temperature is rewarding regarding speed control (default 22)')
    -t3     -- Reference temperature in circuit 3 regarding reward policy, go to simulink model if another reference temperature is rewarding regarding speed control (default 22)')
    -t4     -- Reference temperature in circuit 4 regarding reward policy, go to simulink model if another reference temperature is rewarding regarding speed control (default 22)')
    -lm     -- (Learning Mode) - Q-network will be updated if active (Learning mode is active by default)', choices=[NO])
    -startup--This set Tmix to wanted and all valves if there is any and stops flow to circuits when reference temperatures is met before proceeding with DRL algorithm (No, not active by default)', choices=[YES])
    -Tmix   -- Start mixing temperature is required when using start up')
    -model  -- Model type - DQN is with tensorflow and DQN LSTM is pytorch and DQNELI is with tensorflow (DQN is default)', choices=[DQN, DQNLSTM, DQNELI])  
  
# Required arguments to run on main.py:  
    -model  -- 'torch_dqn, torch_dqnlstm, torch_dqnet is in pytorch and tf_dqnet is in tensorflow (dqn = deep q-network, eli = eligibility_trace)', choices=[TORCH_DQN, TORCH_DQNLSTM, TORCH_DQNET, TF_DQNET], required=True)
    -env    -- 'S=Simulation, E=Experiment, T=Test, L=Level, N=level grade, TL for normal house and everything with E is regarding experimental setup ', choices=[TL12, TL3, TL4, SETL2, SETL3, SETL4, ETL2, ETL3, ETL4], required=True)

Note startup requires Tmix which have to be above 20
    
Forexample, below the user specific specifies that he/she wants tau = 20, and model should be DQN from pytorch with environment model from Test Level 1 or 2.
  
python main.py -tau 20 -model torch_dqn -env tl12
  
  
TCP connect receiver and send port by running Simulink model <TestLevel_X_MODEL.slx>. (notice first time starting Simulation can result in 
no connection to TCP/IP server established by python. Simply just run the script again and start the simulation yet again)