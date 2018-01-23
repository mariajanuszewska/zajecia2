Zajecia2

1. Instrukcje warunkowe
(zmienna <- rnorm(1))
if (zmienna < 0){
  cat("mniejsza ")
}

(zmienna <- rnorm(1))
if (zmienna < 0){
  cat("mniejsza \n")
}else cat("wieksza\n")

(zmienna <- rnorm(1))
if (zmienna < 0 || zmienna^2 > 0.5){
  cat("OK\n") 
}else{
  cat("Nie OK\n")
}
wersja wektorowa:
(zmienna <- rnorm(5))
ifelse(zmienna < 0, "mniejsza", "wieksza")
d <- ifelse(zmienna < 0, "mniejsza", "wieksza")
d

2. Pętle for

for(i in 1:5) {
  cat("aktualna wartosc i to", i, "\n")
}

# 5 razy aktualna wrtosc i to 1/2/3/4/5/

(macierz <- matrix(1:20, 5, 4))
for(i in 1:nrow(macierz))
{
  print(mean(macierz[i,]))
}

#średnia w kolejnych wierszy

3. Petle while
4. Funckje

# NazwaFunkcji <- function(argument1, argument 2) {
  instrukcje (opcjonalnie) return(wynik)}
  MojaFunkcja <- function(a,b) {
  a^2 + b^2
}
MojaFunkcja(1,2)
MojaFunkcja2 <- function(x, y) {
  a <- sin(x)
  b <- cos(y)
  (a+b)^2
}

funkcja zwraca ostatnie wyrazenie domyślnie, ale można zdeklarować co ma zwrócić:
MojaFunkcja3 <- function(x, y) {
  a <- sin(x)
  b <- cos(y)
  wynik <- a*b*100
  print("ala ma kota")
  return(c(a, b*100, wynik))
}
po instrukcji return nic nie jest już wykonywane, np print ()
MojaFunkcja5 <- function(x,y) {paste(x,y)}
MojaFunkcja5("ala", "ma")
MojaFunkcja5(MojaFunkcja5("ala", "ma"), "kota")

# apply
n <- 5
m <- 10
mx <- matrix(data = round(100*runif(n*m, 0, 1), 0), nrow = n, ncol = m)
apply(mx, 1, sum)
apply(mx, 2, sum)

# lapply
example_list <- list(c(0, 1, 2, 3), rep('p', 5), seq(2, 20, 3), runif(20))
length(example_list)
lapply(example_list, length)
lapply(example_list, function(element){
  if (length(element) > 5) 'Wiecej niz 5 elementow' else '5 elementow lub mniej'
})


ZADANIE 1
Wykonaj ponizsze transformacje, za kazdym razem zapisujac posredni wynik do nowej zmiennej
library("tidyverse")
ze zbioru danych wybierz kolumny dotyczace miesiecy, plci, dlugosci i wagi rybek, zapisz wynik jako lw
lw <- select(RuffeSLRH92, month, sex, length, weight)
posortuj dane wedlug miesiecy i plci rybek, zapisz wynik jako ms
ms <- arrange(lw, month, sex)
do zbioru LW dodaj nowa kolumne bedaca logarytmem dlugosci rybek, nazwij ja log_l, wynikowa tabele zapisz jako log_lw
log_lw <- mutate(lw,
                 log_l = log(length))
wskaz liczbe rybek dla kazdego miesiaca i plci, zapisz wynik jako sum_mon_sex
by_mon_sex <- group_by(lw, month, sex)
sum_mon_sex <- summarise(by_mon_sex,
                   count = n())
pogrupuj rybki wg plci i wybierz te grupy, ktorych srednia waga jest wieksza niz 15
by_sex <- group_by(lw, sex)
mean_weight_by_sex <- summarise(by_sex,
                                mean_weight = mean(weight, na.rm = TRUE))
mean_weight_by_sex_above_15 <- filter(mean_weight_by_sex, mean_weight > 15)

Podpunkt b)
Wykonaj ponizsze transformacje, laczac je za pomoca operatora pipeline %>% z pakietu dplyr
ze zbioru danych wybierz kolumny dotyczace miesiecy, plci, dlugosci i wagi rybek
posortuj dane wedlug miesiecy i plci rybek
dodaj nowa kolumne bedaca logarytmem dlugosci rybek, nazwij ja log_l
wskaz liczbe rybek dla kazdego miesiaca i plci, zapisz wynik jako sum_mon_sex

sum_mon_sex <- RuffeSLRH92 %>%
  select(., month, sex, length, weight) %>%
  arrange(., month, sex) %>%
  mutate(., log_l = log(length)) %>%
  group_by(., month, sex) %>%
  summarise(., count = n())
  
  
  
