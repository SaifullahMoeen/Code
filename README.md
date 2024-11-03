# Code
import math
import numpy as np
import matplotlib.pyplot as plt

class ScientificCalculator:
    def __init__(self):
        self.history = []

    def add_to_history(self, operation):
        self.history.append(operation)

    def show_history(self):
        print("\nHistory of calculations:")
        for entry in self.history:
            print(entry)

    def add(self, x, y):
        result = x + y
        self.add_to_history(f"{x} + {y} = {result}")
        return result

    def subtract(self, x, y):
        result = x - y
        self.add_to_history(f"{x} - {y} = {result}")
        return result

    def multiply(self, x, y):
        result = x * y
        self.add_to_history(f"{x} * {y} = {result}")
        return result

    def divide(self, x, y):
        if y == 0:
            return "Error! Division by zero."
        result = x / y
        self.add_to_history(f"{x} / {y} = {result}")
        return result

    def square_root(self, x):
        result = math.sqrt(x)
        self.add_to_history(f"√{x} = {result}")
        return result

    def power(self, x, y):
        result = math.pow(x, y)
        self.add_to_history(f"{x} ^ {y} = {result}")
        return result

    def sine(self, x):
        result = math.sin(math.radians(x))
        self.add_to_history(f"sin({x}) = {result}")
        return result

    def cosine(self, x):
        result = math.cos(math.radians(x))
        self.add_to_history(f"cos({x}) = {result}")
        return result

    def tangent(self, x):
        result = math.tan(math.radians(x))
        self.add_to_history(f"tan({x}) = {result}")
        return result

    def plot_function(self, func, x_range):
        x = np.linspace(x_range[0], x_range[1], 100)
        if func == "sin":
            y = np.sin(x)
        elif func == "cos":
            y = np.cos(x)
        elif func == "tan":
            y = np.tan(x)
        else:
            print("Function not supported for plotting.")
            return

        plt.plot(x, y)
        plt.title(f'Graph of {func}(x)')
        plt.xlabel('x')
        plt.ylabel(f'{func}(x)')
        plt.grid()
        plt.axhline(0, color='black', lw=0.5)
        plt.axvline(0, color='black', lw=0.5)
        plt.show()

    def convert_units(self, value, from_unit, to_unit):
        conversion_factors = {
            "m_to_km": value / 1000,
            "km_to_m": value * 1000,
            "kg_to_g": value * 1000,
            "g_to_kg": value / 1000,
        }
        key = f"{from_unit}_to_{to_unit}"
        return conversion_factors.get(key, "Conversion not supported.")

def main():
    calculator = ScientificCalculator()
    
    while True:
        print("\nOptions:")
        print("1. Add")
        print("2. Subtract")
        print("3. Multiply")
        print("4. Divide")
        print("5. Square Root")
        print("6. Power")
        print("7. Sine")
        print("8. Cosine")
        print("9. Tangent")
        print("10. Plot Function")
        print("11. Unit Conversion")
        print("12. Show History")
        print("0. Exit")
        
        choice = input("Choose an option: ")

        if choice == '0':
            break
        elif choice in ['1', '2', '3', '4']:
            x = float(input("Enter first number: "))
            y = float(input("Enter second number: "))
            operations = {
                '1': calculator.add,
                '2': calculator.subtract,
                '3': calculator.multiply,
                '4': calculator.divide,
            }
            print(f"Result: {operations[choice](x, y)}")
        elif choice == '5':
            x = float(input("Enter number: "))
            print(f"Result: {calculator.square_root(x)}")
        elif choice == '6':
            x = float(input("Enter base: "))
            y = float(input("Enter exponent: "))
            print(f"Result: {calculator.power(x, y)}")
        elif choice in ['7', '8', '9']:
            x = float(input("Enter angle in degrees: "))
            trig_operations = {
                '7': calculator.sine,
                '8': calculator.cosine,
                '9': calculator.tangent,
            }
            print(f"Result: {trig_operations[choice](x)}")
        elif choice == '10':
            func = input("Enter function to plot (sin, cos, tan): ")
            x_min = float(input("Enter x minimum: "))
            x_max = float(input("Enter x maximum: "))
            calculator.plot_function(func, (x_min, x_max))
        elif choice == '11':
            value = float(input("Enter value to convert: "))
            from_unit = input("Enter from unit (m, km, kg, g): ")
            to_unit = input("Enter to unit (m, km, kg, g): ")
            print(f"Converted: {calculator.convert_units(value, from_unit, to_unit)}")
        elif choice == '12':
            calculator.show_history()
        else:
            print("Invalid choice.")

if __name__ == "__main__":
    main()
