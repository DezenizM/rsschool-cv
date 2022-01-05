# Hello, i'm Matvey Obydenov

## Contacts
* **Location:** Russia, Samara
* **Phone:** +79879856057
* **GitHub:** [DezenizM](https://github.com/DezenizM)

## About Me
_My goal is to learn to program in order to try myself in something new. I always try to achieve my goals and easily understand the material that I find._

## Skills
* HTML
* CSS
* Python
* C#

## Code Example
```
import pygame as pg
import numpy as np
import math

#множество Мандельброта строится на основе соотношения, для которого следующее комплексное число
#формируется из суммы куба(в данном случае) предыдущего и некоторого комплексного числа C
# Множество находится в пределах окружности с радиусом равным 2
# Z(n+1) = Zn^3 + C, где Zn, C - комплексные числа, Z0 = 0, модуль |Zn| < 2
# Для построения фрактала :
# - формируем С на основе значений массива screen_array
# - выполняем Z(n+1) = Zn^3 + C заданное кол-во раз(max_iter) или до тех пор пока пока |Z| < 2
# - находим цвет пикселя на основе num_iter/max_iter

# настройки
res = width, height = 600, 800
offset = np.array([1.3 * width, height]) // 2 # массив для переноса системы координат в центр фрактала
max_iter = 40 # максимальное количество итераций
zoom = 2.2 / width # переменная для отображения фрактала в нужном масштабе

# добавляем цвет с помощью градиента
#texture = pg.image.load('img/texture.jpg') # загружаем градиент
#texture_size = min(texture.get_size()) - 1
#texture_array = pg.surfarray.array3d(texture) # преобразуем в numpy массив

class Fractal:
    def __init__(self, app):
        self.app = app
        self.screen_array = np.full((width, height, 3), [0, 0, 0], dtype=np.uint32) #полотно для рисования

    def render(self): #рендер
        for x in range(width): #проходимся по всем координатам с учётом сдвига и масштаба
            for y in range(height):
                c = (x - offset[0]) * zoom + 1j * (y - offset[1]) * zoom #формируем комплексное число C
                z = 0
                num_iter = 0
                for i in range(max_iter):
                    z = z**3 + c #вычисляем Z
                    if abs(z) > 2 : # проверяем абсолютное значение
                        break
                    num_iter += 1

                if num_iter == max_iter :
                    r = g = b = 0
                else :
                    r = (num_iter % 2) * 32 + 128
                    g = (num_iter % 4) * 64
                    b = (num_iter % 2) * 16 + 128
                # в результате цикла мы получаем число пройденных итераций
                #col = int(texture_size * num_iter / max_iter) # формируем с помощью пройденных итераций цвет для текущих координат экрана
                self.screen_array[x, y] = (r, g, b)
                #texture_array[col, col]

    def update(self): #обновление состояния
        self.render()

    def draw(self): #отрисовка
        pg.surfarray.blit_array(self.app.screen, self.screen_array)

    def run(self): #запускающий метод
        self.update()
        self.draw()

class App: # класс задающий окно
    def __init__(self):
        self.screen = pg.display.set_mode(res, pg.SCALED) # SCALED - позволит аппаратно увеличить изображение до текущего изображения экрана
        self.clock = pg.time.Clock()
        self.fractal = Fractal(self) #экземляр фрактала создаём в классе приложения

    def run(self):
        while True:
            self.screen.fill('black')
            self.fractal.run() # запускаем
            pg.display.flip()

            [exit() for i in pg.event.get() if i.type == pg.QUIT]
            self.clock.tick()
            pg.display.set_caption(f'FPS: {self.clock.get_fps() :.2f}')

if __name__ == '__main__':
    app = App()
    app.run()
```

## Education
**University:** Samara National Research University named after academician S.P. Korolev

## English
**B2**