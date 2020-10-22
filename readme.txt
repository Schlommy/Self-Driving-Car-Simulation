This contains the python-unity communication scripts and two sample lane detection models.

# Setup instructions:
	* Read notes first.
	1. Install python 3.7.
	2. For running lanenet install cuda v10 and cudnn v7.6 from nvidia. (Nvidia graphics card required)
	3. In a virtual environment run "pip install -r requirements.txt" with cmd.

# Usage instructions:
	1. Start server.py with following arguments:
		* "--models": lanenet or cv_lane_detector
		* "--display_result": to display the results
	# Example: 
		> python server.py --models lanenet --display_result
	
	2. Open unity and load sampleScene1 from scenes folder.
	3. Run the scene.

# Inserting in another project:
	* Python Files remain unchanged.
	* Copy folder Client Scenes to the new project assets.
	* Install socketio from asset store in unity.
	* In the unity scene, add socketio prefab from prefabs folder inside socketio in assets.
	* Configure the ip, port of socketio prefab (port must be same as python, here 5000)
	* Create empty game object and add the client.cs script to it as component, and add your car camera to this component.

# Notes:
	* Unity version: 2018.3.14f1
	* Remove "tensorflow-gpu" from requirements.txt (inside Python Files folder) if you don't have nvidia graphics card or don't wish to ru lanenet model.
	* Client side scripts are in folder Client Scripts inside Scripts folder in assets.
	* Use unity recorder to record ingame footage for training data.
	* To add new models simply create a script like "lanenet_detector.py" and add to the if/else block in server.py.
	* I haven't implemented any controller scripts in unity. The server sends "instructions" event on each frame to unity, any instructions can be added to the corresponding "data_dict" dictionary.
	* These instructions are sent to the unity and recieved in "client.cs" script. Implement a controller script to make use of these instructions.
	* Read socketio.txt for instructions on socketio.