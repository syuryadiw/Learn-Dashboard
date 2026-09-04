# PT Citra Mulia Inti | Sanggala Corridor Project ----
# Dashboard Pengendalian & Mitigasi Karhutla Berbasis Masyarakat
# Syuryadi Wijaya

# 1. ENVIRONMENT SETUP ----
library(tidyverse)
library(googlesheets4)
library(lubridate)
library(leaflet)
library(plotly)
library(DT)
library(scales)
library(viridis)

gs4_deauth()
sheet_id <- "1-EmuS-LUGuhGc8LTpi9rpXz3YMH2sihUI_9Tg_3qaQs"

# 2. LOAD DATA ----
raw_sosialisasi <- read_sheet(sheet_id, 
                              sheet = "Edukasi & Sosialisasi", 
                              na = c("", "NA", "-"))
raw_aspirasi <- read_sheet(sheet_id, 
                           sheet = "Penggalian Aspirasi", 
                           na = c("", "NA", "-"))
raw_jadwalmembakar <- read_sheet(sheet_id, 
                                 sheet = "Jadwal Membakar", 
                                 na = c("", "NA", "-"))
raw_hotspot <- read_sheet(sheet_id, 
                          sheet = "Hotspot & Aktivitas Pembakaran", 
                          na = c("", "NA", "-"))

# 3. DATA CLEANING ----
clean_sosialisasi <- raw_sosialisasi %>%
  mutate(
    Tanggal = as.Date(Tanggal),
    `Jenis Kelamin` = str_to_title(trimws(as.character(`Jenis Kelamin`))),
    Desa = str_to_title(trimws(as.character(Desa))),
    Dusun = str_to_title(trimws(as.character(Dusun))),
    `Kategori Umur` = factor(`Kategori Umur`, 
                             levels = c("18-25", "26-35", "36-45", "46-55", "55+"), 
                             ordered = TRUE)
  )

clean_aspirasi <- raw_aspirasi %>%
  mutate(
    Tanggal = as.Date(Tanggal),
    Desa = str_to_title(trimws(as.character(Desa))),
    Dusun = str_to_title(trimws(as.character(Dusun))),
    `Luas Lahan` = as.numeric(`Luas Lahan`)
  )

clean_jadwalmembakar <- raw_jadwalmembakar %>%
  select(-starts_with("...")) %>%
  mutate(
    `Tanggal Pembakaran Lahan` = as.Date(`Tanggal Pembakaran Lahan`),
    Desa = str_to_title(trimws(as.character(Desa))),
    Dusun = str_to_title(trimws(as.character(Dusun))),
    x = as.numeric(x),
    y = as.numeric(y),
    `Luas Lahan` = as.numeric(`Luas Lahan`)
  )

clean_hotspot <- raw_hotspot %>%
  mutate(
    Tanggal = as.Date(Tanggal),
    Desa = str_to_title(trimws(as.character(Desa))),
    Dusun = str_to_title(trimws(as.character(Dusun))),
    Latitude = as.numeric(y), 
    Longitude = as.numeric(x)
  )

