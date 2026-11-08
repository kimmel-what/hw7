from functools import wraps

def checker(function):
    @wraps(function)
    def wrapper(*args, **kwargs):
        try:
            result = function(*args, **kwargs)
        except ZeroDivisionError:
            print("На нуль ділити не можна")
        except SyntaxError:
            print("Неправильний вираз")
        except Exception as exc:
            print(f"Проблема: {exc}")
        else:
            print(f"{result}")
            return result

    return wrapper

@checker
def calculate(expression):
    return eval(expression)

while True:
    expression = input("Введіть математичний вираз: ")

    if expression.lower() == "exit":
        print("Калькулятор завершено.")
        break

    calculate(expression)
