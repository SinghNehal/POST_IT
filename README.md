# PostIT

A blockchain-based application in python.

## Instructions to run 

```python
$ pip install -r requirements.txt
```
### Starting Blockchain-node and server

```python
export FLASK_APP=node_server.py
flask run --port 8000
```
![image](https://user-images.githubusercontent.com/58623921/115022297-d5aee480-9eda-11eb-8656-bb45230ddc21.png)

Now one instance of our blockchain node is now up and running at port 8000.

### In another Terminal Window type
```python
python run_app.py
```
![image](https://user-images.githubusercontent.com/58623921/115022383-efe8c280-9eda-11eb-9671-417d523ddfac.png)

The application should be up and running at http://localhost:5000.
![image](https://user-images.githubusercontent.com/58623921/115022351-e3fd0080-9eda-11eb-8d88-54be5c739f09.png)

Here are few screenshots for the application : 
1. Posting some content . 
![image](https://user-images.githubusercontent.com/58623921/115021816-1b1ee200-9eda-11eb-93d9-00bbd305331a.png)

2. Requesting node to mine . 
*  ![image](https://user-images.githubusercontent.com/58623921/115021749-004c6d80-9eda-11eb-9840-66faeaebc38a.png)

3. Resyncing the chain with updated data
![image](https://user-images.githubusercontent.com/58623921/115022041-74871100-9eda-11eb-96b9-3a1ff4bbb7dc.png)

Now for settting up multiple Nodes , and registering them we will be using the ```register_with/```
We will be using cURL requests to register the nodes at port `8001` and ``8002`` with the already running ```8000```.

```flask run --port 8000 & flask run --port 8001```
 
```python
curl -X POST \
http://127.0.0.1:8001/register_with \
-H 'Content-Type: application/json' \
-d '{"node_address": "http://127.0.0.1:8000"}'
```
![image](https://user-images.githubusercontent.com/58623921/115022982-caa88400-9edb-11eb-87cb-124a54a9869d.png)

 Now node at port 8000 is aware about nodes at port 8001 and 8002. Now there will be an active participation in mining process and sync in all nodes.
 
Once all of this done, we can run the application , create transactions (post messages via the web interface), and after mining the transactions all the nodes in the network will update the chain.
So now even if we will make two transactions , one with port 8000 and second with port 8001 , we will be able to see both transactions in our blockchain.
![image](https://user-images.githubusercontent.com/58623921/115031952-617a3e00-9ee6-11eb-80d9-696f21fe8533.png)
Transaction 3,4 were done with port 8001, but since it is registered with port 8000 , we will see chain the transactions mentioned with port 8000 , and 8001 mentioned as peer.

We can see the chain of nodes by the following command :
```
curl -X GET http://localhost:8000/chain
```
Screenshot of the chain of nodes for out current transactions is : 
![image](https://user-images.githubusercontent.com/58623921/115031715-19f3b200-9ee6-11eb-9005-d9e990427228.png)

