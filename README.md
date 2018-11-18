# ML
Описание алгоритма 1NN

Для решения задачи классификации с помощью алгоритма нахождения одного ближайшего соседа нам потребуется: обучающая выборка, 
классифицируемый объект и метрика, в которой мы будем подсчитывать расстояния между точками. Целью алгоритма 
1NN является классификация объекта. 
Шаги алгоритма:
1) Определяем координаты точки, которую будем классифицировать. 
2) ВЫбираем метрику (использую евклидову).
3) Потом расчитываем расстояния от классифицируемой точки до каждой точки обучающей выборки. 
4) Выбираем одну точку обучающей выборки, расстояние до которой от классифицируемой наименьшее, получаем информацию о ее классовой принадлежности. 
5) Определяем классифицируемою точку таким же классом, что и наиближайшая точка. 

Код прграммы:

```html
ONN <- function(xl, z)
{
  orderedXl <- sortObjectsByDist(xl, z)
  n <- dim(orderedXl)[2] - 1

  classes <- orderedXl[1, n + 1]
  counts <- table(classes)

  class <- names(which.max(counts))
  return (class)
}
```


Описание алгоритма kNN

Для решения задачи классификации с помощью алгоритма нахождения k ближайших соседей нам потребуется: обучающая выборка, 
классифицируемый объект и метрика, в которой мы будем подсчитывать расстояния между точками. Целью алгоритма kNN является классификация объекта. 
Шаги алгоритма: 
1) Определяем координаты точки, которую будем классифицировать. 
2) ВЫбираем метрику (использую евклидову).
3) Потом расчитываем расстояния от классифицируемой точки до каждой точки обучающей выборки. 
4) Выбираем k точек обучающей выборки, расстояния до которых от классифицируемой наименьшие,  получаем информацию о классе точек доминирующих среди k бижайших (какого класса точек больше среди k ближайших). 
5) Определяем классифицируемою точку таким же классом, что и k ближайших точек.

Код программы:

```html
kNN <- function(xl, z, k)
{
  orderedXl <- sortObjectsByDist(xl, z)
  n <- dim(orderedXl)[2] - 1
  classes <- orderedXl[1:k, n + 1]
  counts <- table(classes)

  class <- names(which.max(counts))
  return (class)
}
```


Описание алгоритма kwNN

Для решения задачи классификации с помощью алгоритма kwNN нам потребуется: обучающая выборка, классифицируемый объект, 
весовая функция для каждого элемента (вычисляется по формуле w=q^i, где q - произвольная величина, i - порядковый номер объекта) и метрика, в которой мы будем подсчитывать расстояния между точками. Целью алгоритма kwNN является классификация объекта. 
Шаги алгоритма: 
1) Определяем координаты точки, которую будем классифицировать. 
2) ВЫбираем метрику (использую евклидову).
3) Потом расчитываем расстояния от классифицируемой точки до каждой точки обучающей выборки. 
4) Выбираем k точек обучающей выборки, расстояния до которых от классифицируемой наименьшие,  получаем информацию о классе точек доминирующих среди k бижайших с помощью весовой функции. Считаем сумму весов точек одного класса среди k ближайших. 
5) Определяем классифицируемою точку таким же классом, что и класс ближайших точек с наибольшей суммой весов.

Код программы:

```html
kwNN <- function(xl, z, k, q)
{

  orderedXl <- sortObjectsByDist(xl, z)
  n <- dim(orderedXl)[2] - 1

 for(i in 1:k){
    orderedXl[i, 4] <- q^i
}
 types <- c("setosa", "versicolor", "virginica")
 mat <- matrix(data=0, nrow=1, ncol=3)
 colnames(mat) <- types

 a=n+1
 b=n+2
 classes <- orderedXl[1:k, a:b]

 mat[1,1] <- sum(classes[classes$Species=="setosa",2])
 mat[1,2] <- sum(classes[classes$Species=="versicolor",2])
 mat[1,3] <- sum(classes[classes$Species=="virginica",2])

nmbr <- which.max(mat)

class <- types[nmbr]

return (class)
}
```

