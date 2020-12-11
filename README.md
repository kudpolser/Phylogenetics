# Phylogenetics

### Обзор статьи
За основу была взята статья "Phylogenetic and genomic analyses of the ribosomal oxygenases Riox1 (No66) and Riox2 (Mina53) provide new insights into their evolution" Katharina E. Bräuer, Kevin Brockers, Jasmin Moneer, Annette Feuchtinger, Evi Wollscheid-Lengeling, Andreas Lengeling & Alexander Wolf. Для построения филогенетического дерева авторы использовали аминокислотные последовательности белка RIOX1 и RIOX2. Часть данных была взята из базы UNIPROT (указаны ссылки на 11 организмов), а последовательность аминокислот для гидры была получена самостоятельно.

Для построения выравнивания авторы использовали программу MAFFT 7 tool (http://www.ebi.ac.uk/Tools/msa/mafft/), а для построения филогенетического дерева: W-IQ-TREE (Version 1.5.4 at http://iqtree.cibiv.univie.ac.at).

В итоге, получились такие результаты:
![GitHub Logo](/Images/results.png)

### Сбор данных
Я буду строить дерево на основе только одного белка: RIOX1. Это оксигеназа, которая может действовать как гистоновая лизин-деметилаза и рибосомная гистидингидроксилаза. В частности, деметилирует Lys-4 (H3K4me) и Lys-36 (H3K36me) гистона H3, тем самым играя центральную роль в гистоновом коде. Также может играть роль в биогенезе рибосом и в репликации или ремоделировании определенной гетерохроматической области. Участвует в активации транскрипции, индуцированной MYC.

Данные брались из базы данных UniProt. Я собрала все 11 организмов, сслыки на которые были указаны  в статье, плюс добавила последовательность для гидры, которую приложили авторы. Также нашла часть организмов, последовательность белка у которых была проверена, то есть ограничислась на данные Swiss-Prot. В итоге, получилось 20 организмов:
1. Bos_taurus (Bovine)
2. Caenorhabditis_elegans (Nematoda)
3. Canis_lupus_familiaris (Dog)
4. Danio_rerio (Zebrafish)
5. Delphinapterus_leucas (Beluga whale)
6. Drosophila_melanogaster (Fruit fly)
7. Felis_catus (Cat)
8. Gallus_gallus (Chicken)
9. Homo_sapiens (Human)
10. Hydra_vulgaris (Hydra)
11. Loxodonta_africana (African elephant)
12. Monodelphis_domestica (Gray short-tailed opossum
13. Mus_musculus (Mouse)
14. Myotis_lucifugus (Little brown bat)
15. Oryzias_latipes (Japanese killifish)
16. Papio_anubis (Olive baboon)
17. Physeter_macrocephalus (Sperm whale)
18. Rattus_norvegicus (Rat)
19. Sus_scrofa (Pig)
20. Xenopus_laevis (African clawed frog)

Чтобы объединить все последовательности в один файл воспользовалась командой cat:
```
$ cat *.fasta > All.fasta
```

### Построение выравнивания

Загрузила данные в MEGAX. Авторы статьи воспользовались алгоритмом MAFFT для построения выравнивнивания, поэтому я решила запустить MUSCLE. 

Так выглядит получившееся выравнивание:
![GitHub Logo](/Images/alignment.png)

Сохранила его в файл All_alignment.fasta в этом репозитории.

### Филогенетическое дерево

Построить дерево можно прямо в программе MEGAX. Я запустила построение дерева с помощью метода максимального правдоподобия с бустрепом. Параметры приведены ниже в таблице:

| Parameter | Value |
| ------------- | ----- |
| Statistical Method | Maximum Likelihood |
| Test of Phylogeny | Bootstrap method |
| No. of Bootstrap Replications | 100 |
| Substitutions Type | Amino acid |
| Model/Method | Poisson model |
| ML Heuristic Method | Nearest-Neighbor-Interchange (NNI) |
| Initial Tree for ML | Make initial tree automatically (Default - NJ/BioNJ) |

Получилось такое дерево:

![GitHub Logo](/Images/tree_meme.png)

Для каждого узла посчитано число в деревьев, в которых это разбиение встречалось. Так как всего использовалось 100 повторений, то числа близкие к этому максимуму будут говорить о высокой значимости такого разбиения.

Также я решила попробовать построить дерево с помощью программы FASTME. Она требует на вход матрицу расстояний, а не просто выравнивания, поэтому пришлось дополнительно поставить пакет EMBOSS. Полученная матрица также лежит в репозитории

```
$ conda install -c bioconda fastme
$ conda install -c bioconda emboss
$ distmat All_alignment.fasta dist_matrix.txt
$ fastme -i dist_matrix.txt
```

С помощью FASTME получилось такое дерево (строчка в формате newick лежит в репозитории, визуализация сделана в MEGA):

![GitHub Logo](/Images/tree_fastme.png)
### Сравнение результатов

Для удобства сравнения разместила все три дерева рядом (последнее изображение - это часть дерева из статьи):
![GitHub Logo](/Images/all_tree.png)

Все используемые мной алгоритмы хорошо предсказывали разделение по отрядам: приматы, грызуны, киты всегда находились вместе. Явно выделяется группа млекопитающих, рыб, отдельно от них находится курица, лягушка, муха и нематода. FASTME, оставил неразрешенность в четверке организмов: гидра, лягушка и два вида рыб. Также различия двух методов возникли в положения летучей мыши и в кладе слон, собака, кошка. В остальном деревья одинаковые. Следует отметить, что различия возникли в узлах с низкой поддержкой бутсрепа, что было ожидаемо. 

Основной вопрос возникает относительно положения гидры. В статье она находится далеко от хордовых, в моем же случае она замешана к ним. Думаю, проблема в том, что в моем анализе не было организмов, разделявших гидру, рыб и земноводных, как в статье. Возможно, они бы заняли эту нишу, создав разрыв между этими животными.
