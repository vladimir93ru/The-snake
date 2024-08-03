# The-snake
Чтобы реализовать проверку корректности выбранного направления, нам нужно добавить несколько функций и переменных.

Во-первых, нам нужно добавить переменную, которая будет хранить текущее направление змейки.

enum direction {
    LEFT,
    RIGHT,
    UP,
    DOWN
};

Затем, нам нужно добавить функцию, которая будет проверять корректность выбранного направления:

int isValidDirection(enum direction currentDirection, enum direction newDirection) {
    if (currentDirection == LEFT && newDirection == RIGHT) return 0;
    if (currentDirection == RIGHT && newDirection == LEFT) return 0;
    if (currentDirection == UP && newDirection == DOWN) return 0;
    if (currentDirection == DOWN && newDirection == UP) return 0;
    return 1;
}

Эта функция принимает текущее направление змейки и новое направление, и возвращает 1, если новое направление корректно, и 0, если нет.

Теперь, нам нужно добавить функцию, которая будет обрабатывать нажатие клавиш и менять направление змейки:

enum direction handleKey(enum direction currentDirection) {
    char key;
    key = getch();
    switch (key) {
        case 'w':
        case 'W':
            if (isValidDirection(currentDirection, UP)) return UP;
            break;
        case 's':
        case 'S':
            if (isValidDirection(currentDirection, DOWN)) return DOWN;
            break;
        case 'a':
        case 'A':
            if (isValidDirection(currentDirection, LEFT)) return LEFT;
            break;
        case 'd':
        case 'D':
            if (isValidDirection(currentDirection, RIGHT)) return RIGHT;
            break;
        default:
            return currentDirection;
    }
    return currentDirection;
}

Эта функция принимает текущее направление змейки, читает нажатую клавишу, и возвращает новое направление змейки, если оно корректно.

Наконец, нам нужно изменить функцию main, чтобы она использовала эти новые функции:

int main(){
    struct snake_t snake = initSnake( 10, 5, 2);
    enum direction direction = LEFT;
    printSnake(snake);
    while(1) {
        direction = handleKey(direction);
        switch (direction) {
            case LEFT:
                snake = moveLeft(snake);
                break;
            case RIGHT:
                snake = moveRight(snake);
                break;
            case UP:
                snake = moveUp(snake);
                break;
            case DOWN:
                snake = moveDown(snake);
                break;
        }
        sleep(1);
        system("cls");
        printSnake(snake);
    }
    return 0;
}
