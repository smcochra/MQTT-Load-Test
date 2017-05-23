# MQTT-Load-Test
Load test showing MQTT delay.

Test may be used or modified. Original use case was to see messaging delay based on number of thread's opened
while attempting to view all or a subset of those threads on the subscription side.

Threads opened is NUM_UUT * NUM_THREAD_PER_UUT
Threads subscribed to is NUM_TEST_PER_UI
NUM_UI_VIEWERS will continue to subscribe to the same threads in NUM_TEST_PER_UI

Edit following parameters to stress test your configuration

NUM_UUT = 40
NUM_THREAD_PER_UUT = 3
NUM_UI_VIEWERS = 5
NUM_TESTS_PER_UI = 10  # should be less than NUM_UUT

SEND_DELAY = 0.2  # sleep time between publishes from NUM_THREAD_PER_UUT * NUM_UUT threads
QOS = 1  # Quality of service for broker to prioritize subscriptions and publishes

# IP/Port of broker to be hosting 
BROKER_ADD = '10.130.41.48'
BROKER_PORT = 1883


                            _____               _____               _____
  NUM_UI_VIEWERS           | UI_1|             | UI_2|             | UI_N|         /|\     Delay in seconds printed upon arrival here
                           |_____|             |_____|       ...   |_____|          |
                            / | \               / | \               / | \           |
                           /  |  \             /  |  \             /  |  \         /|\    Note: each line here represents NUM_THREAD_PER_UUT
                          /   |   \           /   |   \           /   |   \         |
						 /    |    \         /    |    \         /    |    \        |
                       __     __    __      __     __    __     __     __    __    /|\
  NUM_TESTS_PER_UI	  |__|   |__|  |__|    |__|   |__|  |__|   |__|   |__|  |__|    |
					  /|\    /|\   /|\     /|\    /|\   /|\    /|\    /|\   /|\     |
  NUM_THREAD_PER_UUT / | \	/ | \ / | \	  / | \	 / | \ / | \  / | \	 / | \ / | \   /|\	
					_____________________________________________________________   |
                   |                                                             |  |  1-way Send Direction
                   |                            BROKER                           | /|\
                   |                                                             |  |
                   |_____________________________________________________________|  |
                         \  |  /            \  |  /            \  |  /             /|\
  NUM_THREAD_PER_UUT	  \ | /              \ | /              \ | /               | 
	     				   \|/                \|/                \|/                | 
						  _____               _____              _____             /|\
  NUM_UUT           	 | UUT1|             | UUT2|            | UUTN|             |
                         |_____|             |_____|       ...  |_____|				|	 
						 
						 
						 
						 
						 
						 
						 
						 
						 
						 