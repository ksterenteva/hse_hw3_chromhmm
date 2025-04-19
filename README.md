# hse_hw3_chromhmm

[Ссылка на гугл коллаб](https://colab.research.google.com/drive/1gk7-38t-0awgpMGkk0WG8GbP_jDq1fgl?authuser=2#scrollTo=zap-6PjQKi9x)

 Целью данной работы является разбивка генома человека hg19 на разные типы эпигенетических состояний с помощью программы ChromHMM на основе данных чтений, полученных в ChIP-seq экспериментах из проекта ENCODE. Клеточная линия - H1 hesc. Это будет сделано на основании данных о наличии различных гистоновых модификаций (гистоновый код) в соответствующих участках генома. 

 | Гистоновая метка | bam файл           | Контроль             |
|--------------|------------------------------|-----------------------------|
| H3k09me3     | H3k09me3StdAlnRep1.bam       | ControlStdAlnRep1.bam       |
| H3k4me1      | H3k4me1StdAlnRep1.bam        | ControlStdAlnRep1.bam       |
| H3k4me2      | H3k4me2StdAlnRep1.bam        | ControlStdAlnRep1.bam       |
| H3k4me3      | H3k4me3StdAlnRep1.bam        | ControlStdAlnRep1.bam       |
| H3k27ac      | H3k27acStdAlnRep1.bam        | ControlStdAlnRep1.bam       |
| H3k27me3     | H3k27me3StdAlnRep1.bam       | ControlStdAlnRep1.bam       |
| H3k36me3     | H3k36me3StdAlnRep1.bam       | ControlStdAlnRep1.bam       |
| H3k79me2     | H3k79me2StdAlnRep1.bam       | ControlStdAlnRep1.bam       |
| H4k20me1     | H4k20me1StdAlnRep1.bam       | ControlStdAlnRep1.bam       |
| H2az         | H2azStdAlnRep1.bam           | ControlStdAlnRep1.bam       |

### Выдача ChromHMM
<p align="center">
  <img src="https://github.com/user-attachments/assets/eb91213a-46eb-415d-ad0b-6112ae05e529" alt="emissions_10" width="18%">
  <img src="https://github.com/user-attachments/assets/66a5c149-699c-4591-900e-0588fdbb0070" alt="transitions_10" width="18%">
  <img src="https://github.com/user-attachments/assets/a2d83b69-d6f8-4bbd-bf00-7e85caab10d1" alt="H1hesc_10_overlap" width="18%">
  <img src="https://github.com/user-attachments/assets/e40a84a4-6cd8-4742-93da-f2df3fd445d7" alt="TSS" width="18%">
  <img src="https://github.com/user-attachments/assets/062ae31e-1eba-480b-a41c-663cc34e00b9" alt="TES" width="18%">
</p>



| Состояние | Основные метки                          | Обогащение по аннотациям генома         | Поведение на TSS/TES                         | Предполагаемая функция       |
|-----------|------------------------------------------|------------------------------------------|----------------------------------------------|-------------------------------|
| 1         | H3K36me3 (слабый сигнал)         | экзоны, аннотированные гены, окончания генов | – по TSS, сильный сигнал TES, включая участки до и после - транскрибируемые регионы (gene body)                                           |  Тело гена (Transcribed region)  |
| 2         | -                                | аннотированные гены, немного экзоны,концы генов, очень слабо ядерные ламины                   | слабый сигнал по TES                     |  Слабая транскрипция             |
| 3         | H3K79me2                         | только аннотированные гены                             | -                                     |  Слабая транскрипция         |
| 4         | H3K79me2, H3K4me2, H3K4me3       | ±5кб от начала транскрипции, гены, слабее сигналы экзонов, окончания генов                   | Пик после TSS - начало транскрипции, обогащение по TES - транскрибируемые регионы                             |    Слабая транскрипция         |
| 5         | H3K4me2, H3K4me3                 | CpG острова, экзоны, старт транскрипции, ±5кб от начала транскрипции, слабые сигналы по генам и окончанию генов                        | сильный пик на TSS - промоторная активность, сигнал до TES и убывает после 0           |   Активный промотор       |
| 6         | H3K4me2, H3K4me2 (слабый сигнал) | Слабое обогащение по всему кроме % генома                        | cлабый сигнал перед TSS - может быть энхансер, слабый сигнал по TES                                   | Слабый промотор / слабый энхансер    |
| 7         | H2az (средний сигнал)            | Ламина                   | -                |  Инсулятор / структурно стабилизированный участок             |
| 8         | -                                | Ядерная ламина, большой % в геноме!               | -                |  Гетерохроматин          |
| 9         | H3K09me3 (слабый сигнал)         | Ядерная ламина               | слабый сигнал по TES                              | Гетерохроматин (репрессированный)   |
| 10        | H3K27me3                         | окончание генов, слабый сигнал по: CpGIsland (часто совпадают с промоторами), экзоны, аннотированные гены, ±5кб от начала транскрипции, ламина                      | Ровный фон слабый по TSS, средний по TES                                   |  Polycomb-репрессия    |

### UCSC GenomeBrowser
<p align="center">
  <img src="https://github.com/user-attachments/assets/a96a1a12-06b4-4324-a185-28b1b157f773" alt="Снимок экрана 2025-04-13 в 23 14 33" width="33%">
  <img src="https://github.com/user-attachments/assets/84e75b46-e478-47b6-a96a-2797bf392777" alt="Снимок экрана 2025-04-15 в 22 51 51" width="33%">
  <img src="https://github.com/user-attachments/assets/0b028b24-a7ec-49ab-bd17-735aefafe8f1" alt="Снимок экрана 2025-04-15 в 22 52 39" width="33%">
</p>

### UCSC GenomeBrowser с названиями эпигенетических типов

<img width="1372" alt="Снимок экрана 2025-04-15 в 23 00 00" src="https://github.com/user-attachments/assets/331c7462-0f52-4cf9-91c4-4d2946b303a3" />

## Бонус 

Оценка качества эпигенетической аннотации, полученной с помощью ChromHMM, с использованием SAGAconf показала, что большинство состояний обладают высокой стабильностью.

Наиболее стабильными оказались состояния 7 (R² = 0.995), 5 (0.86), 8 (0.85) и 0 (0.81)

Только двум типам (3 (0.35) и 9 (0.38)) нельзя доверять тк имеют низкую воспроизводимость 

В целом, полученные значения R² указывают на высокую воспроизводимость модели, что подтверждает надёжность предсказаний ChromHMM на выбранных данных.


<img width="401" alt="Снимок экрана 2025-04-20 в 02 22 07" src="https://github.com/user-attachments/assets/19f4819d-f5e9-4c05-bc46-b0f32637a01d" />

