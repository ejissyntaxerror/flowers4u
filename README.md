# flowers4u
from PIL import Image, ImageDraw, ImageSequence
import random
import os

# Function to draw a flower
def draw_flower(draw, center_x, center_y, petal_color, center_color):
    # Draw petals
    num_petals = 8
    angle = 0
    angle_increment = 360 / num_petals
    radius = 20
    for _ in range(num_petals):
        x = center_x + int(radius * random.uniform(0.7, 1.3) * math.cos(math.radians(angle)))
        y = center_y + int(radius * random.uniform(0.7, 1.3) * math.sin(math.radians(angle)))
        draw.polygon([(x, y), (center_x, center_y), (x, y)], fill=petal_color)
        angle += angle_increment

    # Draw center
    draw.ellipse((center_x - 5, center_y - 5, center_x + 5, center_y + 5), fill=center_color)

# Function to create a frame of the GIF
def create_frame(width, height):
    image = Image.new('RGB', (width, height), (255, 255, 255))
    draw = ImageDraw.Draw(image)

    # Draw multiple flowers
    num_flowers = random.randint(3, 5)
    for _ in range(num_flowers):
        center_x = random.randint(50, width - 50)
        center_y = random.randint(50, height - 50)
        petal_color = (random.randint(100, 255), random.randint(100, 255), random.randint(100, 255))
        center_color = (random.randint(0, 50), random.randint(150, 255), random.randint(0, 50))
        draw_flower(draw, center_x, center_y, petal_color, center_color)

    return image

# Main function to create the GIF
def create_bouquet_gif(output_path, num_frames, frame_duration, width=400, height=400):
    frames = []
    for _ in range(num_frames):
        frame = create_frame(width, height)
        frames.append(frame)
    
    # Save as GIF
    frames[0].save(output_path, format='GIF', append_images=frames[1:], save_all=True, duration=frame_duration, loop=0)

# Example usage
if _name_ == "_main_":
    output_path = 'flower_bouquet.gif'
    num_frames = 20
    frame_duration = 200  # in milliseconds

    create_bouquet_gif(output_path, num_frames, frame_duration)
    print(f'GIF saved to {output_path}')
