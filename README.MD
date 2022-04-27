js is single threaded so has only one execution stack.
cluster module allow to use multy core.
it helps to create child process which shares server port here 3000.
worker processes are spawned using fork() method.
once forked this processes can communicate with master process using IPC channel. hence can pass the
messages from master to child processes and vice versa.
cluster module support 2 method to distribute incoming connection.
1> round robin(master process listen on port accept incomming connection and distribute in round robin fashion) default across all plateform except windows
2> second method(master process creates the listen socket and send to interested workers, and worker accept incomming connection directly).

CLUSTER MODULE OFFER TWO CLASS CLUSTER AND WORKER::::
a1>>> CLUSTER EVENTS, METHODS AND PROPERTIES:
1> EVENTS: online, fork, message, disconnect, exit etc.
2> METHODS: disconnect, fork etc.
3> PROPERTIES: isMaster, isWorker etc.
a> online event==when new worker forked by master,this worker should respond with online message & master emit received.
b> when new worker is forked, cluster module emmit an forked event, used to log worker activity and create custom timeout.
c> when cluster master receive message from worker, message event gets emitted.
d> disconnect event get's trigger when worker IPC channel to master disconnects.
e> exit event emitted when worker dies to restart need to fork again.
f> fork method spawn worker process and can only be called from master.
g> you have to call disconnect method from each worker process.


a2>>> WORKER CLASS EVENTS, METHODS AND PROPERTIES:
1> EVENTS: online, message, disconnect, exit etc.
2> METHODS: disconnect, isConnected, isDead, kill, send etc.
3> PROPERTIES: id, process etc.
a> in master disconnect method disconnect worker servers and wait for close event and disconnect the IPC channel.
b> send method helps worker pass message to master.

HOW TO GET CPU COUNT? gives number of array of logical cpus core in our system.
os.cpus()  and os.cpus().length

to perform load test on our customn cluster we can use loadtest or artillery install using npm any one. using
this tool you dont have to do multiple request from browser rather you can test your application from terminal with as many reques, no of concurrent req, and request per second twiking look npm registery for those package.
-my preferred load testing tool is loadtest so use that rather than artillery.









