# Phylogenetics

### Обзор статьи
За основу была взята статья "Phylogenetic and genomic analyses of the ribosomal oxygenases Riox1 (No66) and Riox2 (Mina53) provide new insights into their evolution" Katharina E. Bräuer, Kevin Brockers, Jasmin Moneer, Annette Feuchtinger, Evi Wollscheid-Lengeling, Andreas Lengeling & Alexander Wolf. Для построения филогенетического дерева авторы использовали аминокислотные последовательности белка RIOX1 и RIOX2. Часть данных была взята из базы UNIPROT (указаны ссылки на 11 организмов), а последовательность аминокислот для гидры была получена самостоятельно.

Для построения выравнивания авторы использовали программу MAFFT 7 tool (http://www.ebi.ac.uk/Tools/msa/mafft/), а для построения филогенетического дерева: W-IQ-TREE (Version 1.5.4 at http://iqtree.cibiv.univie.ac.at).

В итоге, получились такие результаты:
![GitHub Logo](/Images/results.png)

### Сбор данных
Я буду строить дерево на основе только одного белка: RIOX1. Это оксигеназа, которая может действовать как гистоновая лизин-деметилаза и рибосомная гистидингидроксилаза. В частности, деметилирует Lys-4 (H3K4me) и Lys-36 (H3K36me) гистона H3, тем самым играя центральную роль в гистоновом коде. Также может играть роль в биогенезе рибосом и в репликации или ремоделировании определенной гетерохроматической области. Участвует в активации транскрипции, индуцированной MYC.

Данные брались из базы данных UniProt. Я собрала все 11 организмов, сслыки на которые были указаны, плюс добавила последовательность для гидры, которую авторы приложили к статье. Там же нашла еще часть организмов, последовательность белка у которых была провеврена, то есть ограничислась на данные Swiss-Prot. В итоге, получилось 20 организмов:
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

### Построение выравнивания
![GitHub Logo](/Images/alignment.png)
### Филогенетическое дерево
![GitHub Logo](/Images/tree.png)
### Сравнение результатов
