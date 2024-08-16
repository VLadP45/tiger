# tigerfrom pydub import AudioSegment
from pydub.playback import play
import numpy as np

def generate_tiger_roar():
    sample_rate = 44100
    
    # Define the parameters for the roar sound
    duration_ms = 1000  # duration of the roar
    base_freq = 80  # base frequency for the roar (low frequency for deep sound)
    noise_amplitude = 0.5  # amplitude of the noise
    decay_factor = 0.3  # how quickly the roar fades out
    
    t = np.linspace(0, duration_ms / 1000, int(sample_rate * duration_ms / 1000), False)
    
    # Generate a base tone (low frequency sine wave)
    base_tone = np.sin(2 * np.pi * base_freq * t)
    
    # Generate noise and add it to the base tone
    noise = noise_amplitude * np.random.normal(size=t.shape)
    roar_wave = base_tone + noise
    
    # Apply a decay to simulate the roar fading out
    roar_wave *= np.exp(-decay_factor * t)
    
    # Convert to 16-bit audio format
    audio = np.int16(roar_wave * 32767)
    
    # Create an audio segment from the generated roar
    tiger_roar = AudioSegment(audio.tobytes(), frame_rate=sample_rate, sample_width=2, channels=1)
    
    return tiger_roar

# Generate the tiger roar sound
tiger_roar = generate_tiger_roar()

# Play the tiger roar sound
play(tiger_roar)
