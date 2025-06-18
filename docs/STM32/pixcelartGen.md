# 串口打印像素画生成器

```

from PIL import Image

# ASCII characters from darkest to lightest
ASCII_CHARS = ["@", "#", "S", "%", "?", "*", "+", ";", ":", ",", "."]

def resize_image(image, new_width=100):
    width, height = image.size
    ratio = height / width / 1.65  # Adjust ratio to maintain aspect ratio
    new_height = int(new_width * ratio)
    resized_image = image.resize((new_width, new_height))
    return resized_image

def grayify(image):
    return image.convert("L")

def pixels_to_ascii(image):
    pixels = image.getdata()
    ascii_str = ""
    for pixel_value in pixels:
        ascii_str += ASCII_CHARS[pixel_value // 25]  # Map pixel value to ASCII
    return ascii_str

def main():
    path = "input.jpg"
    try:
        image = Image.open(path)
    except Exception as e:
        print(f"Unable to open image file {path}.")
        print(e)
        return

    image = resize_image(image)
    image = grayify(image)

    ascii_str = pixels_to_ascii(image)
    img_width = image.width
    ascii_str_len = len(ascii_str)
    ascii_img = ""

    # Format the string to match image width
    for i in range(0, ascii_str_len, img_width):
        ascii_img += ascii_str[i:i+img_width] + "\n"

    print(ascii_img)

if __name__ == "__main__":
    main()
    # To print the image in color, we can use ANSI escape codes for colored output.
    # This requires mapping each pixel to a color and printing it.

    def colorize_ascii(image):
        pixels = image.getdata()
        width, height = image.size
        ascii_img = ""

        for y in range(height):
            for x in range(width):
                r, g, b = image.getpixel((x, y))
                # ANSI escape code for RGB color
                ascii_img += f"\033[38;2;{r};{g};{b}m█"
            ascii_img += "\033[0m\n"  # Reset color and add newline

        return ascii_img

    def main_color():
        path = "input.jpg"
        try:
            image = Image.open(path)
        except Exception as e:
            print(f"Unable to open image file {path}.")
            print(e)
            return

        image = resize_image(image)

        # Print the colorized ASCII image
        ascii_img = colorize_ascii(image)
        print(ascii_img)
            # Scale down the image by half and print again
        scaled_image = image.resize((image.width // 3, image.height // 3))
        scaled_ascii_img = colorize_ascii(scaled_image)
        print(scaled_ascii_img)
        # Scale down the image further by half and print with 256-color ANSI codes
        scaled_image_256 = image.resize((image.width // 2, image.height // 2))
        scaled_ascii_img_256 = ""
        
        for y in range(scaled_image_256.height):
            for x in range(scaled_image_256.width):
                r, g, b = scaled_image_256.getpixel((x, y))
                # Convert RGB to 256-color ANSI code
                color_code = 16 + (36 * (r // 51)) + (6 * (g // 51)) + (b // 51)
                scaled_ascii_img_256 += f"\x1b[48;5;{color_code}m "
            scaled_ascii_img_256 += "\x1b[0m\n"  # Reset color and add newline
        
        print(scaled_ascii_img_256)


        scaled_ascii_img_256 = ""
        
        for y in range(scaled_image_256.height):
            scaled_ascii_img_256 += "printf(\""  # Reset color and add newline

            for x in range(scaled_image_256.width):
                r, g, b = scaled_image_256.getpixel((x, y))
                # Convert RGB to 256-color ANSI code
                color_code = 16 + (36 * (r // 51)) + (6 * (g // 51)) + (b // 51)
                scaled_ascii_img_256 += f"\\x1b[48;5;{color_code}m "
            scaled_ascii_img_256 += "\\x1b[0m\\n\");\n"  # Reset color and add newline
            # scaled_ascii_img_256 = scaled_ascii_img_256.replace("\n", "\\n")
        with open("resize256color.c", "w") as f:
            f.write(scaled_ascii_img_256)

     
    if __name__ == "__main__":
        main_color()
      
```