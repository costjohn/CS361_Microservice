# CS361_Microservice



To connect with the microservice you will need to send and receive using the ZeroMQ/pyzmq library. You would need
something similar to the below in the main program, but make sure the port (if locally) matches the microservice's port.

import zmq
context = zmq.Context()
socket = context.socket(zmq.REQ)
socket.connect("tcp://localhost:5556")

**
How to programmatically REQUEST data:**
The following information is needed to return the correct dilution volume:

1. starting concentration mass unit 
2. starting concentration volume unit
3. starting concentration 

4. starting volume unit 
5. starting volume 

6. desired mass unit 
7. desired liquid unit 
8. desired concentration 

Possible mass units: “g, mg, ug, ng”
Possible volume units: “L, mL, uL”

It must be written as a string with "/" between each value in order for the microservice to correctly recognize each value. 
So the string would be as follows, where the number corresponds to the value above "1/2/3/4/5/6/7/8"

If any of it is out of order or "/" is not used, the microservice return an error.

<b><u>As an example: </u> </B>
starting concentration mass unit: mg 

starting concentration volume unit: uL

starting concentration: 100

starting volume unit: mL

starting volume: 20

desired mass unit: g

desired liquid unit: mL

desired concentration: 5

the string to send would therefore be: "mg/uL/100/mL/20/g/mL/5"

We would send using socket/zmq:
socket.send(b"mg/uL/100/mL/20/g/mL/5")

<b>How to programmatically RECEIVE data:</b>

To receive data you must have the following code. The variable name can be changed however it suits your program.
dilutionResult = socket.recv()


<b>UML Diagram</b>

<img width="1259" alt="image" src="https://github.com/costjohn/CS361_Microservice/assets/86116449/059e4278-5f52-4e94-b68d-5134c5c8f38d">
