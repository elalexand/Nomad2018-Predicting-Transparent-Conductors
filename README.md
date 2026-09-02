# NOMAD2018 — Band Gap Prediction

Проект по предсказанию **band gap energy** (и formation energy) прозрачных проводящих оксидов на основе данных соревнования [NOMAD2018 Kaggle Challenge: Predicting Transparent Conductors](https://www.kaggle.com/c/nomad2018-predict-transparent-conductors).

Модель обучается на кристаллографических данных материалов (Al–Ga–In оксиды) и предсказывает две целевые переменные:
- `formation_energy_ev_natom` — энергия образования на атом (эВ/атом)
- `bandgap_energy_ev` — ширина запрещённой зоны (эВ)

## Содержание

- [Описание задачи](#описание-задачи)
- [Данные](#данные)
- [Метрика качества](#метрика-качества)


## Описание задачи

Прозрачные проводящие оксиды (TCO) используются в солнечных панелях, сенсорных экранах и светодиодах. Задача — найти материалы с оптимальным сочетанием прозрачности (широкий band gap) и проводимости, используя только геометрию кристаллической решётки и состав, без дорогостоящих DFT-расчётов.

Каждый образец описывается:
- химическим составом (доли Al, Ga, In)
- параметрами элементарной ячейки (a, b, c, α, β, γ)
- пространственной группой
- количеством атомов
- файлом геометрии `geometry.xyz` с координатами атомов


## Данные

Данные скачиваются с [страницы соревнования на Kaggle](https://www.kaggle.com/c/nomad2018-predict-transparent-conductors/data) и распаковываются в `data/`:

```bash
kaggle competitions download -c nomad2018-predict-transparent-conductors -p data/
unzip data/nomad2018-predict-transparent-conductors.zip -d data/
```


## Метрика качества

Соревнование оценивалось по **RMSLE** (Root Mean Squared Logarithmic Error), усреднённой по обеим целевым переменным:

```
RMSLE = sqrt( mean( (log(1 + y_pred) - log(1 + y_true))^2 ) )
```
