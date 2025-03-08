import streamlit as st
import pandas as pd
import numpy as np

st.title("Clustering")

df_power = pd.read_csv('super_hero_powers.csv')
st.header("Tabela dos poderes dos super heróis", divider="blue")
st.dataframe(df_power)

df_information = pd.read_csv('heroes_information.csv')
st.header("Tabela das informações dos heróis", divider="blue")
st.dataframe(df_information)

st.header("Estatísticas descritivas para a tabela dos poderes dos super heróis", divider="blue")
var_power = st.multiselect(
    "Selecione as variáveis de interesse:",
    options = df_power.columns.values,
    default=['Agility']
)
df_power2 = df_power[var_power].copy()
st.dataframe(df_power2.describe())

st.header("Distribuições das variáveis para a tabela dos poderes dos super heróis", divider="blue")
for value in var_power:
    st.subheader(value, divider="grey")
    hist_values = np.histogram(
        df_power[value], bins=24, range=(0,24))[0]
    st.bar_chart(hist_values)

st.header("Estatísticas descritivas para a tabela das informações dos heróis", divider="blue")
var_info = st.multiselect(
    "Selecione as variáveis de interesse:",
    options = df_information.columns.values,
    default=['Gender']
)
df_information2 = df_information[var_info].copy()
st.dataframe(df_information2.describe())

st.header("Filtragem dos heróis por Alinhamento", divider="blue")
alinhamento = st.radio(
    "Qual o alinhamento que você quer escolher para o herói?",
    options = df_information['Alignment'].unique(),
    index=None
)
df_alinhamento = df_information[df_information['Alignment']==alinhamento]
st.dataframe(df_alinhamento)

st.header("Filtragem dos heróis por Gênero", divider="blue")
genero = st.radio(
    "Qual o gênero que você quer escolher para o herói?",
    options = df_information['Gender'].unique(),
    index=None
)
df_genero = df_information[df_information['Gender']==genero]
st.dataframe(df_genero)

st.header("Filtragem dos heróis por Editora", divider="blue")
editora = st.radio(
    "Qual a editora que você quer escolher para o herói?",
    options = df_information['Publisher'].unique(),
    index=None
)
df_editora = df_information[df_information['Publisher']==editora]
st.dataframe(df_editora)