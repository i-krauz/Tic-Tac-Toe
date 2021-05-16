print("---------")
print("| " + " " + " " + " " + " " + " " + " |")
print("| " + " " + " " + " " + " " + " " + " |")
print("| " + " " + " " + " " + " " + " " + " |")
print("---------")

list_of_numbers = ["1", "2", "3", "4", "5", "6", "7", "8", "9", "0"]
user_input = list("_" * 9)
input_matrix = [[user_input[0], user_input[1], user_input[2]],
                [user_input[3], user_input[4], user_input[5]],
                [user_input[6], user_input[7], user_input[8]]]
result = "Game not finished"
turn = 0


def input_coordinates():
    print("Enter the coordinates: ")
    coords = input()
    coords = coords.split(" ")
    global coord1
    coord1 = coords[0]
    if len(coords) == 1:
        global coord2
        coord2 = ""
    else:
        coord2 = coords[1]

    if coord1 not in list_of_numbers or coord2 not in list_of_numbers:
        print("You should enter numbers!")
        input_coordinates()
    elif int(coord1) > 3 or int(coord2) > 3:
        print("Coordinates should be from 1 to 3!")
        input_coordinates()
    elif int(coord1) < 1 or int(coord2) < 1:
        print("Coordinates should be from 1 to 3!")
        input_coordinates()
    elif input_matrix[int(coord1) - 1][int(coord2) - 1] != "_":
        print("This cell is occupied! Choose another one!")
        input_coordinates()
    return(coord1, coord2)


while result == "Game not finished":
    input_coordinates()
    turn += 1
    if turn % 2 == 1:
        input_matrix[int(coord1) - 1][int(coord2) - 1] = "X"
        new_step1 = ("".join(input_matrix[0]))
        new_step2 = ("".join(input_matrix[1]))
        new_step3 = ("".join(input_matrix[2]))

        new_step = new_step1 + new_step2 + new_step3

        print("---------")
        print("| " + new_step[0] + " " + new_step[1] + " " + new_step[2] + " |")
        print("| " + new_step[3] + " " + new_step[4] + " " + new_step[5] + " |")
        print("| " + new_step[6] + " " + new_step[7] + " " + new_step[8] + " |")
        print("---------")
    if turn % 2 == 0:
        input_matrix[int(coord1) - 1][int(coord2) - 1] = "O"
        new_step1 = ("".join(input_matrix[0]))
        new_step2 = ("".join(input_matrix[1]))
        new_step3 = ("".join(input_matrix[2]))

        new_step = new_step1 + new_step2 + new_step3

        print("---------")
        print("| " + new_step[0] + " " + new_step[1] + " " + new_step[2] + " |")
        print("| " + new_step[3] + " " + new_step[4] + " " + new_step[5] + " |")
        print("| " + new_step[6] + " " + new_step[7] + " " + new_step[8] + " |")
        print("---------")

    only_x = [_ for _ in new_step if _ == "X"]
    only_o = [_ for _ in new_step if _ == "O"]
    only_empty = [x for x in new_step if x == "_"]

    x_wins = 0
    o_wins = 0
    total_wins = 0

    for i in range(3):
        if input_matrix[0][i] != "_" and input_matrix[0][i] == input_matrix[1][i] == input_matrix[2][i]:
            total_wins += 1
            if input_matrix[0][i] == "X":
                x_wins += 1
            else:
                o_wins += 1
        if input_matrix[i][0] != "_" and input_matrix[i][0] == input_matrix[i][1] == input_matrix[i][2]:
            total_wins += 1
            if input_matrix[i][0] == "X":
                x_wins += 1
            else:
                o_wins += 1
    if input_matrix[1][1] != "_" and input_matrix[0][0] == input_matrix[1][1] == input_matrix[2][2]:
        total_wins += 1
        if input_matrix[1][1] == "X":
            x_wins += 1
        else:
            o_wins += 1

    if input_matrix[1][1] != "_" and input_matrix[0][2] == input_matrix[1][1] == input_matrix[2][0]:
        total_wins += 1
        if input_matrix[1][1] == "X":
            x_wins += 1
        else:
            o_wins += 1

    if abs(len(only_x) - len(only_o)) >= 2:
        result = "Impossible"
        print(result)
    elif total_wins > 1:
        result = "Impossible"
        print(result)
    elif total_wins == 0 and len(only_empty) == 0:
        result = "Draw"
        print(result)
    elif x_wins == 1:
        result = "X wins"
        print(result)
    elif o_wins == 1:
        result = "O wins"
        print(result)
    elif total_wins == 0 and len(only_empty) > 0:
        result = "Game not finished"
   
