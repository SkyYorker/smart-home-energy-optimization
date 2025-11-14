# Система оптимизации энергопотребления умного дома с Deep Q-Learning

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/SkyYorker/smart-home-energy-optimization/blob/main/smart-home-energy-optimization.ipynb)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)

Интеллектуальная система управления энергопотреблением в умном доме на основе алгоритмов глубокого обучения с подкреплением (Deep Q-Learning). Проект реализует оптимизацию использования электроприборов с учетом тарифов, погодных условий и доступности солнечной энергии.

## Описание проекта

Проект представляет собой исследовательскую работу по применению алгоритма Deep Q-Network (DQN) для оптимизации энергопотребления в умном доме. Система обучается минимизировать стоимость электроэнергии, учитывая:

- **Однотарифный учет**: 3.47 руб/кВт·ч (для Чебоксар, 2025)
- **Сезонные колебания температуры**: динамическая модель температурных условий
- **Доступность солнечной энергии**: учет солнечной генерации и накопительных батарей
- **Комфорт жильцов**: поддержание оптимальной температуры в помещении

## Основные возможности

- **Custom DQN реализация**: Алгоритм Deep Q-Learning с PyTorch для работы с MultiDiscrete пространством действий
- **Сравнение алгоритмов**: Реализованы DQN, PPO и A2C для сравнения эффективности
- **Визуализация обучения**: Графики наград, loss, epsilon и Q-значений
- **Сохранение чекпойнтов**: Автоматическое сохранение лучших моделей (локально и в Google Drive)
- **Реалистичная среда**: Имитационная модель умного дома с Gymnasium

## Быстрый старт

### Вариант 1: Google Colab (рекомендуется)

1. Откройте блокнот `smart-home-energy-optimization.ipynb` в Google Colab
2. Выполните ячейки по порядку
3. Все зависимости установятся автоматически

### Вариант 2: Локально

1. Клонируйте репозиторий:
```bash
git clone https://github.com/SkyYorker/smart-home-energy-optimization.git
cd smart-home-energy-optimization
```

2. Создайте виртуальное окружение:
```bash
python -m venv venv
source venv/bin/activate  # Linux/Mac
# или
venv\Scripts\activate  # Windows
```

3. Установите зависимости:
```bash
pip install -r requirements.txt
```

4. Откройте блокнот в Jupyter:
```bash
jupyter notebook "smart-home-energy-optimization.ipynb"
```

## Структура проекта

```
smart-home-energy-optimization/
├── smart-home-energy-optimization.ipynb      # Основной блокнот с полной реализацией
├── requirements.txt                          # Зависимости проекта
├── README.md                                 # Документация (этот файл)
├── LICENSE                                   # MIT лицензия
├── .gitignore                                # Игнорируемые файлы
└── .gitattributes                            # Настройки Git для UTF-8
```

## Технологический стек

- **Reinforcement Learning**: 
  - Custom DQN (PyTorch)
  - Stable-Baselines3 (PPO, A2C)
- **Фреймворк**: Gymnasium (OpenAI Gym)
- **Глубокое обучение**: PyTorch
- **Визуализация**: Matplotlib, Plotly, Seaborn
- **Обработка данных**: NumPy, Pandas

## Результаты

После обучения агент демонстрирует:
- Оптимизацию использования электроприборов с учетом тарифов
- Учет доступности солнечной генерации
- Поддержание комфортной температуры в помещении
- Минимизацию стоимости электроэнергии

## Архитектура системы

### Пространство состояний (State)
- Время суток (час)
- Температура внутри помещения (°C)
- Температура снаружи (°C)
- Тариф на электроэнергию (руб/кВт·ч)
- Доступность солнечной генерации (кВт)
- Уровень накопительной батареи (%)
- Присутствие людей (0/1)

### Пространство действий (Action)
- Отопление (выкл/эконом/турбо)
- Бойлер (вкл/выкл)
- Кондиционер (вкл/выкл)
- Зарядка электромобиля (вкл/выкл)

### Функция награды (Reward)
```
Reward = -(Стоимость_энергии) + Бонусы_за_комфорт + Бонусы_за_солнечную_энергию + Бонусы_за_умное_использование
```

## Обучение модели

### Гиперпараметры DQN:
- Learning rate: 1e-3
- Gamma (discount factor): 0.99
- Epsilon: 1.0 → 0.01 (decay: 0.995)
- Batch size: 32
- Memory size: 10000
- Target network update frequency: каждые 10 эпизодов

### Процесс обучения:
1. Сбор опыта через взаимодействие со средой
2. Сохранение в replay buffer
3. Обучение на случайных батчах
4. Периодическое обновление target network
5. Уменьшение exploration rate (ε-decay)

## Автор

**Косых Александр Сергеевич**
- Email: skyyorker@gmail.com
- GitHub: [github.com/skyyorker](https://github.com/skyyorker)

## Лицензия

Этот проект лицензирован под MIT License - см. файл [LICENSE](LICENSE) для деталей.



