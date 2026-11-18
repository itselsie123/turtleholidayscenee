# turtleholidayscenee


import turtle
import random

# Setup screen
screen = turtle.Screen()
screen.setup(width=800, height=600)
screen.title("Cozy Winter Holiday Scene")
screen.bgcolor("#111a2e")  # Midnight blue sky
screen.tracer(0)  # Turns off animation for instant drawing

# Initialize turtle
t = turtle.Turtle()
t.hideturtle()
t.speed(0)


def draw_rectangle(x, y, width, height, color):
    """Helper function to draw filled rectangles."""
    t.penup()
    t.goto(x, y)
    t.pendown()
    t.color(color)
    t.begin_fill()
    for _ in range(2):
        t.forward(width)
        t.left(90)
        t.forward(height)
        t.left(90)
    t.end_fill()


def draw_background():
    """Function 1: Draws the snowy ground landscape and night stars."""
    # Draw snowy ground (White half-circle/rectangle)
    draw_rectangle(-400, -300, 800, 150, "#f0f4f8")

    # Draw sky stars using a loop
    t.color("#ffffff")
    for _ in range(30):
        star_x = random.randint(-400, 400)
        star_y = random.randint(-100, 280)
        t.penup()
        t.goto(star_x, star_y)
        t.pendown()
        t.begin_fill()
        for _ in range(5):
            t.forward(5)
            t.right(144)
        t.end_fill()


def draw_cabin(x, y):
    """Function 2: Draws a cozy holiday cabin using specific x, y parameters."""
    # Main house body (Brown Square)
    draw_rectangle(x, y, 120, 100, "#6e473b")

    # Door (Dark Red)
    draw_rectangle(x + 45, y, 30, 60, "#a63a2b")

    # Door knob (Yellow Circle)
    t.penup()
    t.goto(x + 70, y + 30)
    t.pendown()
    t.color("#fcc419")
    t.begin_fill()
    t.circle(3)
    t.end_fill()

    # Window (Warm Yellow Glowing Square)
    draw_rectangle(x + 15, y + 40, 20, 20, "#ffe066")
    draw_rectangle(x + 85, y + 40, 20, 20, "#ffe066")

    # Roof (Red Triangle)
    t.penup()
    t.goto(x - 10, y + 100)
    t.pendown()
    t.color("#c92a2a")
    t.begin_fill()
    t.goto(x + 60, y + 150)
    t.goto(x + 130, y + 100)
    t.goto(x - 10, y + 100)
    t.end_fill()


def draw_holiday_tree(x, y, size):
    """Function 3: Draws a decorated holiday tree at a specific x, y coordinate."""
    # Trunk
    draw_rectangle(x - 10, y, 20, 30, "#42281d")

    # Tree Layers (Green Triangles)
    current_y = y + 20
    layer_width = size
    for i in range(3):
        t.penup()
        t.goto(x - layer_width / 2, current_y)
        t.pendown()
        t.color("#2b8a3e")
        t.begin_fill()
        t.goto(x, current_y + (size * 0.6))
        t.goto(x + layer_width / 2, current_y)
        t.goto(x - layer_width / 2, current_y)
        t.end_fill()

        # Generate colorful ornaments on the tree edges using loops
        t.color(random.choice(["#e03131", "#15aabf", "#fab005", "#e599f7"]))
        t.penup()
        t.goto(x - layer_width / 4, current_y + 10)
        t.pendown()
        t.begin_fill()
        t.circle(4)
        t.end_fill()

        t.penup()
        t.goto(x + layer_width / 4, current_y + 10)
        t.pendown()
        t.begin_fill()
        t.circle(4)
        t.end_fill()

        # Adjust dimensions for the next layer up
        current_y += (size * 0.4)
        layer_width *= 0.8

    # Tree Star (Gold)
    t.penup()
    t.goto(x - 7, current_y + 5)
    t.pendown()
    t.color("#fab005")
    t.begin_fill()
    for _ in range(5):
        t.forward(14)
        t.right(144)
    t.end_fill()


if __name__ == "__main__":
    # 1. Render static background
    draw_background()

    # 2. Draw the holiday cabin using the x, y parameter function
    draw_cabin(-250, -150)

    # 3. Draw a small forest of holiday trees at different sizes and coordinates
    draw_holiday_tree(50, -150, 100)
    draw_holiday_tree(180, -130, 120)
    draw_holiday_tree(290, -160, 90)

    # Refresh screen to show the complete picture instantly
    screen.update()

    # Keep window open cleanly
    turtle.done()
