This project is an Arduino-based Morse code input device that uses a simple touch sensor to translate taps into decoded text. By tapping on a wire or a conductive surface connected to the device, a user can input Morse code, which is then translated and printed to the serial monitor in real-time. This project combines fundamental electronics, C++ programming, and an understanding of communication protocols to create an interactive and educational tool.

How It Works
Hardware Setup: The core of the project is an ESP32 microcontroller, which has built-in capacitive touch sensing capabilities. A single touch pin (T4) is connected to a conductive surface (like a wire or a piece of metal foil). The ESP32's touchRead() function measures the capacitance of this surface. When a finger touches it, the value drops, signaling a tap.

Morse Code Input: The program's loop() function constantly monitors the touch pin.

Detecting Taps: When a touch is detected (the touchValue falls below a set TOUCH_THRESHOLD), the program records the start time.

Differentiating Dots and Dashes: When the touch is released, the program calculates the duration of the tap. A short tap (less than DASH_THRESHOLD) is interpreted as a "dot" (.), while a longer tap is a "dash" (-). These dots and dashes are appended to a string called currentMorseCode.

Decoding Logic: After each tap, the program waits for a pause. The length of this pause determines how the dots and dashes are grouped:

Inter-Character Space: If a pause is longer than INTER_CHAR_SPACE_THRESHOLD, it signals the end of a single Morse code character. The program then looks up the currentMorseCode string in a std::map that stores all Morse code combinations and their corresponding characters (e.g., "-.-" maps to 'K'). The decoded character is added to a decodedText string and printed to the serial monitor.

Inter-Word Space: A much longer pause, exceeding WORD_SPACE_THRESHOLD, is interpreted as a space between words. The program adds a space to the decodedText, allowing for the transcription of complete sentences.

Output: All decoded characters are printed to the serial monitor, creating a real-time log of the message being "tapped" by the user

This project was fun making and implementing. Nowadays almost no one uses Morse code as it takes up so much time even to type in one word making this a fun but useless project. 