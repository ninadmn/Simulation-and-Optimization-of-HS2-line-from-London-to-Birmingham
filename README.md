# Simulation-and-Optimization-of-HS2-line-from-London-to-Birmingham
Simulation and optimisation of  London HS2 using simpy 


## The Context
A high-speed train as planned for the HS2 line from London to Birmingham has an acceleration
of 0.72m/s2
, about the same as a commuter train. While the trains can brake in an emergency
at 2.5m/s2
, the energy optimal deceleration (using regenerative braking) is 0.36m/s2
.

The maximum travelling speed of the train is about 300km/h (83.3m/s). Accelerating from 0
to the maximum speed takes therefore 115.7s during which time the train travels about
4,820m. Slow decelerating takes 231.4s and the distance travelled is 9,640m.
A railway line consists of a sequence of signaling blocks. A train is only allowed to enter a
block, when there is no other train in the block and the entry signal is green. When a train
enters a block the entry signal switches to red. The entrance signal switches back to green 5
seconds after the end of the train has left the block.
Depending on the intended maximum traveling speed there is an optimal distance for setting
a pre-signal. At a maximum travelling speed of the train of 300km/h (83.3m/s) the slow
deceleration takes 231.4s and the train travels 9,640m during this time. In this case the presignal would be 10km before the actual signal at the end of one block and the entry to the next. The length of a block should therefore be at least 10km, but to allow a train to achieve and run as long as possible at full speed, the block length should be at least 1.5x this length.
The control problem is to keep the trains moving at maximum possible speed. If there is a slight delay in one train it may cause the train in the following block to decelerate, potentially down to a stop, and then to reaccelerate. This in turn will delay the train thereafter. Just like the “traffic jam” effect you know from the motorway. A train can run constantly at full speed if there is always at least one free block ahead. With a block length of 15km that means that the distance between two trains should be about 30km, at full speed a travelling time of about 6min. This would indicate that one could achieve a maximum schedule of 10 trains per hour. The new government under Boris Johnson is pushing the development of HS2. The economic
argument is based on a schedule time of 9 trains per hour. 



## Part 1: Simulation

Create a simulation for the London-Birmingham section of the high-speed line under
assumption of a number k of signalling blocks. A decision on the number of signaling blocks is
required, as the track laying is supposed to start soon. Also a decision on the number of trains
running per hour has to be made.


Depending on the number of signalling blocks simulate the throughput of trains.
Take into account that between Birmingham Interchange and Birmingham Curzon street as
well as between London Old Oak Common and London Euston there will be a practical speed
limit and the traveling times are 5 min between London Euston and London Old Oak Common
(one signalling block) and 9 min between Birhigham Interchange and Birmingham Curzon
Street station (two signalling blocks). Take into account the variability of achievable speeds
due to wind and weather conditions on the stretch between London Old Oak Common and
Birmingham Interchange. Take into account the variability in stop times, i.e. minor delays due
to passenger movements.

London Euston
 5 min
London Old Oak Common
 31 min
Birmingham Interchange
 9 min
Birmingham Curzon Street
The distance between London Old Oak Common Station and Birmingham Interchange Station
is 145km. This could be broken down in up-to 14 blocks. If there are less but longer blocks the
trains could achieve in theory a higher average speed, however the throughput in trains per hours is smaller.

Part 2: Optimisation
For the project you need to create a simulation of the train network which would give for a
given train schedule (numbers of trains per hour n ∈ {1, 2, 3, 4, 5, 6, 8, 10, 12, 15, 20}) and a
given break-down of the line in signalling blocks k ∈ {1, ..., 15} a distribution of average
overall travelling time. The simulation results are fed into an optimisation problem to
determine (nopt, kopt) to achieve an optimal results.
Using the simulation described above solve the following optimisation problems:
(1)Minimise the overall average traveling time.
The overall traveling time consist of the waiting time for the next train and the
actual traveling time until arrival of the train. The problem can be simplified by
assuming a fixed average waiting time (0.5*60/n).
(2)Maximise the throughput of passengers in peak hours.
The trains can be configured to run at a length of 200m (short train, 420 passengers)
or 300m (max train, 630 passengers). While longer trains carry potentially more
passengers, you need to consider the walking times at the train station. The walking
speed of a train passenger carrying luggage is between 1.0 and 1.2m/s, which
impacts on the stop times at the station. Also more passengers disembarking and
embarking may lengthen the stop times.
For a more realistic simulation assume a Poisson-Distribution for passengers arriving
at the train station at an average rate of m passengers per hour and how they can
be served by n trains per hour. As the trains are on a tight schedule, we cannot
assume that everyone gets on board during the short stopping time. Assume that
the trains are only filled to 70% of nominal capacity. A backlog of passengers on the
departing station will impact on the average travelling time.
