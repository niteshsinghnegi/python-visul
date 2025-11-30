from vpython import *
import math
import time

scene.title = "Animated 3D Objects"
scene.width = 800
scene.height = 600

# -------------------------------
# FUNCTIONS TO CREATE OBJECTS
# -------------------------------

def make_curve():
    pts = []
    for t in range(400):
        ang = t * 0.1
        x = math.cos(ang)
        y = math.sin(ang)
        z = ang * 0.05
        pts.append(vector(x, y, z))
    c = curve(points=pts, radius=0.05, color=color.cyan)
    return c

def make_sphere():
    return sphere(pos=vector(0,0,0), radius=1, color=color.red)

def make_cone():
    return cone(pos=vector(0,-1,0), axis=vector(0,2,0), radius=0.8, color=color.green)

def make_arrow():
    return arrow(pos=vector(-2,0,0), axis=vector(4,0,0), shaftwidth=0.2, color=color.yellow)

def make_ring():
    return ring(pos=vector(0,0,0), axis=vector(0,1,0), radius=1.2, thickness=0.2, color=color.magenta)

def make_cylinder():
    return cylinder(pos=vector(0,-1,0), axis=vector(0,2,0), radius=0.6, color=color.blue)


# -------------------------------
# ANIMATION LOOP
# -------------------------------

def animate(obj, obj_type):
    print("\nAnimation running... Close window to stop.\n")

    t = 0
    while True:
        rate(60)
        t += 0.03

        if obj_type == "curve":
            obj.rotate(angle=0.02, axis=vector(0,1,0))
        
        elif obj_type == "sphere":
            obj.rotate(angle=0.03, axis=vector(0,1,0))
        
        elif obj_type == "cone":
            obj.rotate(angle=0.03, axis=vector(0,1,0))
        
        elif obj_type == "cylinder":
            obj.rotate(angle=0.03, axis=vector(1,0,0))
        
        elif obj_type == "arrow":
            obj.pos.x = math.sin(t) * 2  # oscillation movement
        
        elif obj_type == "ring":
            obj.rotate(angle=0.04, axis=vector(0,0,1))


# -------------------------------
# MENU
# -------------------------------

def menu():
    print("\n--- MENU ---")
    print("1. Curve (animated)")
    print("2. Sphere (rotating)")
    print("3. Cone (rotating)")
    print("4. Arrow (moving)")
    print("5. Ring (rotating)")
    print("6. Cylinder (rotating)")
    print("0. Exit")

# -------------------------------
# MAIN PROGRAM LOOP
# -------------------------------

while True:

    menu()
    ch = int(input("Enter choice: "))

    if ch == 0:
        print("Exiting...")
        break

    scene.delete()  # clear old objects

    if ch == 1:
        obj = make_curve()
        animate(obj, "curve")

    elif ch == 2:
        obj = make_sphere()
        animate(obj, "sphere")

    elif ch == 3:
        obj = make_cone()
        animate(obj, "cone")

    elif ch == 4:
        obj = make_arrow()
        animate(obj, "arrow")

    elif ch == 5:
        obj = make_ring()
        animate(obj, "ring")

    elif ch == 6:
        obj = make_cylinder()
        animate(obj, "cylinder")

    else:
        print("Invalid choice!")
