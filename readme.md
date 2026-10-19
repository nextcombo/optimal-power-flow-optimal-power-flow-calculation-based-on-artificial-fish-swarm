# [Optimal Power Flow] Optimal Power Flow Calculation Based on Artificial Fish Swarm Algorithm (Matlab Code Implementation)

​  
Editor: Optimal Power Flow (OPF) is when the structural parameters and load are given, by controlling variable optimization, to find a solution that can satisfy all
Specify the constraints and achieve optimal power flow distribution when one or more performance indicators of the system are optimized. The optimal power flow algorithm can be roughly divided into classical solution algorithms and modern optimization methods.
The classic solution algorithm mainly refers to the methods based on linear programming and non-linear programming, as well as decoupling principles, represented by simplified gradient method, Newton's method, interior-point method, and decoupling method. Its characteristic is to utilize the objective function to solve the first or second order derivative of control variables. When the search starting point is within the convergence domain of local optima, it often falls into the local optimum.
Modern optimization algorithms are constructed on a certain intuitive foundation and are also known as heuristic algorithms. They include Genetic Algorithms (GA), Simulated Annealing, etc.
Algorithms such as SA (Simulated Annealing) and SO (Particle Swarm Optimization) offer new approaches and methods for solving complex problems due to their unique advantages and mechanisms. Currently, they are mainly applied to large-scale nonlinear optimization problems that traditional mathematical optimization methods struggle with. Heuristic algorithms are independent of derivatives, do not require assumptions or approximations, possess randomness, easily escape local extremum points, and have inherent parallelism, significantly enhancing the speed of processing complex optimization problems.
Based on the Artificial Fish Swarm Algorithm (AFSA), this paper proposes an optimal power flow calculation method.
A new method.
The Artificial Fish Swarm Algorithm is a stochastic search optimization algorithm based on the behavior of fish schools, primarily utilizing the foraging, clustering, and tail chasing behaviors of fish.
Starting from the bottom-level behavior of constructing a single fish, this algorithm aims to emerge in the group by achieving the global optimum through local optimization among individual fish within the population. Computational examples demonstrate that this algorithm possesses strong capabilities to overcome local extremities and attain global extremities.
1.1 Optimal Power Flow Problem Editor
Editor
1) Foraging behavior: Generally, fish swim randomly and freely in the water. When they detect food, they will quickly swim towards the direction where the food is increasing.
2. Grouping behaviors: Fish naturally form groups during their swimming to ensure their own survival and avoid potential threats. The rules they follow include: separation rules, minimizing crowding with neighboring partners; alignment rules, aiming for an average directional alignment with nearby partners; inclusive rules, moving towards the center of the group formed by nearby partners.
3. Following behavior: When one or several fish in a school discover food, their kin nearby will follow them rapidly to the food source.
Editor
Editor
Editor
The Artificial Fish Swarm Algorithm seeks the minimum on clustering, cohesion, and crowding, while maximizing food concentration, gradually moving forward in search optimization. That is, each iteration, artificial fish move towards the minimum direction for N steps, with smaller N leading to higher precision in optimization but slower speed; larger N leads to faster optimization but can result in oscillations at certain levels, affecting the accuracy of optimization. The objective function is a complex nonlinear function, and conventional optimization algorithms easily fall into local minima or oscillate between extreme values without convergence, resulting in poor optimization performance. However, genetic algorithms and other algorithms introduce longer computational times. Applying the Artificial Fish Swarm Algorithm effectively overcomes these shortcomings.
Editor
📚2 Running Results Editing
Part of the code:
Load data1.txt; % Existing branch data
Load data2.txt; % Selected branch data
Load data3.txt; % Node power
tic,  
data1=data1;  
data2=data2;  
data3=data3;  
[N,row]=size(data3); %N is the number of nodes
fish=40; % Control parameters: Number of artificial fishes.
visual=7; % control parameter: field of view
delta=0.35;  % Control parameter: Crowding degree
step=5;    % Control parameter: Step size for artificial fish movement
maxcalculation=100;  % Convergence condition: Maximum number of iterations
objectvalue=zeros(1,fish);  % Food concentration matrix (1×fish)
[NN,row]=size(data2);  % NN is the dimension of the selected line
status=rand(fish,NN);  % Position state matrix of artificial fish status
for i=1:fish  
    for j=1:NN  
        if status(i,j)<=0.5  
            status(i,j)=0;  
        else  
            status(i,j)=1;  
        end  
    end  
end  
minvalue=inf;  
for fishnumber=1:fish  
    x=status(fishnumber,:);  
    [B1,B,BL,NEW,NL,L,nbl]=builtnet(x,data2,data1);  
    [tong]=liantong(N,L,BL);  
    if tong>1  
        objectvalue(fishnumber)=inf;  
    else  
        [operate,overflowvalue]=dcflow(N,L,BL,data3,nbl);  
        construction=0;  
        for i=1:NEW  
            construction=construction+25*B1(i,6);  % Calculate construction cost per kilometer of line construction cost is taken as 250,000 yuan
        end  
    end  
end
objectvalue(fishnumber)=construction+operate+overflowvalue;  
end  
if objectvalue(fishnumber)<minvalue  
minvalue=objectvalue(fishnumber); % minvalue records the smallest objective function value.
minfish = status(fishnumber, :); % minfish records the position of artificial fish corresponding to the minimum target function value.
end  
end  
% Implement behavioral strategies
calculation=1;  
while calculation<maxcalculation  
for fishnumber=1:fish  
[status,objectvalue,swarmflag]=swarm(status,fishnumber,objectvalue,visual,fish,NN,N,delta,step,data2,data1,data3);  
if swarmflag==0  
[status,objectvalue,followflag]=follow(status,fishnumber,objectvalue,visual,fish,NN,N,delta,step,data2,data1,data3);  
if followflag==0  
[status,objectvalue]=prey(status,fishnumber,objectvalue,visual,fish,NN,N,delta,step,data2,data1,data3);  
end  
end  
end  
🌈3 Matlab code + data + explanation
🎉4 References
​  

## Images

![[Optimal Power Flow] Optimal Power Flow Calculation Based on Artificial Fish Swarm Algorithm (Matlab Code Implementation)](01.gif)
![[Optimal Power Flow] Optimal Power Flow Calculation Based on Artificial Fish Swarm Algorithm (Matlab Code Implementation)](02.png)
![[Optimal Power Flow] Optimal Power Flow Calculation Based on Artificial Fish Swarm Algorithm (Matlab Code Implementation)](03.png)
![[Optimal Power Flow] Optimal Power Flow Calculation Based on Artificial Fish Swarm Algorithm (Matlab Code Implementation)](04.png)
![[Optimal Power Flow] Optimal Power Flow Calculation Based on Artificial Fish Swarm Algorithm (Matlab Code Implementation)](05.png)
![[Optimal Power Flow] Optimal Power Flow Calculation Based on Artificial Fish Swarm Algorithm (Matlab Code Implementation)](06.png)
![[Optimal Power Flow] Optimal Power Flow Calculation Based on Artificial Fish Swarm Algorithm (Matlab Code Implementation)](07.png)
![[Optimal Power Flow] Optimal Power Flow Calculation Based on Artificial Fish Swarm Algorithm (Matlab Code Implementation)](08.png)
![[Optimal Power Flow] Optimal Power Flow Calculation Based on Artificial Fish Swarm Algorithm (Matlab Code Implementation)](09.png)

<!-- PAYMENT_BLOCK -->

## Get this dataset

- Payment link (Stripe): [Buy now](https://buy.stripe.com/3cs8yP7sY87d0vu9AB)
- Payment QR code: ![Payment QR code](pay.png)

<!-- /PAYMENT_BLOCK -->
