
Overview of changes in the code:
In the original 'orig.da' code following variables were included delay message, loss rate, wait time, proposer and learner timeouts and number of repetitions. Lets see what changes these variabes bring:
1) Delay Message(d) : This determines the delay in sending the message upto d secs. This was implemented using sleep method.
2) Loss Rate(r) : This determines the loss of messages in the channel. This was implemented using random function, logic behind the implementation was that whenever the random fucntion genreated value greater than loss rate only then message was to be sent.
3) wait time(w) : This was included to wait for w secs before trying new round this was implemented using sleep method.
4) proposer and learner timeout(tp & tl) : This determines the timeouts for proposer and learner in secs. This was implemented by replacing TIMEOUT variable by timeout method. 
5) number of repetitions(n): This was included to repeate each run n times so that its statistic could be generated. 

A class 'isSafe' is included in orig.da to check the safety condition. Our final file with above changes is called orig_updated.da

To implement preemption we extented this modified orig.da and added condition for preeption. This file is called orig_preempt.da 
Preemption changes on acceptor side was that if it had any 'n' greater than proposed n1 then it would send preemption to n1 proposer.
Preemption changes on proposer side was that after sending prepare message if any preemption message is recieved then don't wait for response of prepare message start proposal with next higher proposal number.
  

Running the code:
To run the program do the following:
1. copy main.da, orig.da and orig_preempt.da in the same folder.
2. from command line type command 'dar' main.da <<provide parameters>>
3. In <<provide parameters>> pass all the paramenters like nacceptors, nproposers,
	nlearners, n, r, d, w, tp, tl

Sample command will be: dar main.da 10 5 10 1 0.1 0 1 5 5

Some Notes:
1. If dar command is not accepteded then use "python -m da" in place of "dar".
2. Also in main.da the point where :
						child = subprocess.Popen(['dar',.....
   replace by following:
						child = subprocess.Popen(['Python -m da' .....
3. If permission error occurs set permission to 'rwx' for each of the file using,
	command: chmod 777 <<file name>>

Comparisons.xlsx has been attached, it included time comparisons for different values of parmeters and inferences based on the results.


Assignment discussed with: Dhruv Suri.
