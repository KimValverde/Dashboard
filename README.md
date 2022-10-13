# Dashboard
import pandas as pd
import streamlit as st
import matplotlib.pyplot as plt

st.set_page_config(
    page_title="Pacientes con cancer",
    page_icon=None,
    layout="centered",
    initial_sidebar_state="collapsed",
    menu_items=None)

st.title ("Introducción a la programación")
st.header ("Proyecto 1")
st.subheader ("Barrantes, G y Valverde, K")
st.text("En la siguiente pagina podra buscar graficos con respecto al cancer de seno")
st.text("a partir de un estudio realizado por SEER Program of the NCI en el 2017.")
st.write("Para ver los datos originales [link](https://www.kaggle.com/datasets/reihanenamdari/breast-cancer)")
st.text("INSTRUCCIONES: abra la pestaña al lado izquierdo y seleccione la variable que quiere visualizar en el gráfico")


datos = pd.read_csv("Breast_Cancer.csv")

st.sidebar.title("Edad vs Grado de cancer")
st.expander("imagen")
st.image("imagen.jpg")


edad_grado = sorted(datos["Age"].unique())
boton_edad_grado = st.sidebar.selectbox("Grado de cancer asociado a la edad", options = edad_grado)

col1, = st.columns(1)
 


with col1:
    st.header("Grado de cancer acorde la edad")
    dph = datos[datos["Age"] == boton_edad_grado]
    fig, ax =plt.subplots()
    ax.hist(dph["Grade"],color = "pink", edgecolor = "black")
    ax.set_title(f"Edad {boton_edad_grado}")
    ax.set_xlabel("Grado de cancer")
    st.pyplot(fig)

st.sidebar.title("Tamaño del tumor vs Grado")
ts = datos["Grade"].unique()
boton_tam_siz = st.sidebar.selectbox("Tamaño del tumor asociado al grado", options = ts )

col2, = st.columns(1)

with col2:
    st.header("Tamaño del tumor vs Grado")
    dph = datos[datos["Grade"] == boton_tam_siz ]
    fig, ax =plt.subplots()
    ax.hist(dph["Tumor Size"],color = "pink", edgecolor = "white")
    ax.set_title(f"Grado {boton_tam_siz}")
    ax.set_xlabel("Tamaño")
    ax.set_ylabel("Personas")
    st.pyplot(fig)
    
    
