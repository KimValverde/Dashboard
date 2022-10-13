import pandas as pd
import streamlit as st
import matplotlib.pyplot as plt
import plotly.express as px

st.set_page_config(
    page_title="Pacientes con cancer",
    page_icon=None,
    layout="centered",
    initial_sidebar_state="expanded",
    menu_items=None)


datos = pd.read_csv("Breast_Cancer.csv")

Graficos = ("Inicio","Grado de cancer acorde la edad","Tamaño del tumor asociado al grado","Prueba")
Menu = st.sidebar.selectbox("Menu", options = (Graficos))

if Menu == "Inicio":
    st.title ("Introducción a la programación")
    st.header ("Proyecto 1")
    st.subheader ("Barrantes, G y Valverde, K")

    st.text("En la siguiente pagina podra buscar graficos con respecto al cancer de seno")
    st.text("a partir de un estudio realizado por SEER Program of the NCI en el 2017.")
    st.write("Para ver los datos originales [link](https://www.kaggle.com/datasets/reihanenamdari/breast-cancer)")
    st.text("INSTRUCCIONES: abra la pestaña al lado izquierdo y seleccione en Menu la variable que quiere visualizar en el gráfico.")
    st.expander("imagen")
    st.image("imagen.jpg")

if Menu == "Grado de cancer acorde la edad":

    edad_grado = sorted(datos["Age"].unique())
    boton_edad_grado = st.sidebar.selectbox("Grado de cancer asociado a la edad", options = edad_grado)
    st.header("Grado de cancer acorde la edad")
    dph = datos[datos["Age"] == boton_edad_grado]
    fig, ax =plt.subplots()
    ax.hist(dph["Grade"],color = "pink", edgecolor = "black")
    ax.set_title(f"Edad {boton_edad_grado}")
    ax.set_xlabel("Grado de cancer")
    st.pyplot(fig)
if Menu == "Tamaño del tumor asociado al grado":

    ts = datos["Grade"].unique()
    boton_tam_siz = st.sidebar.selectbox("Tamaño del tumor asociado al grado", options = ts )
    st.header("Tamaño del tumor vs Grado")
    dph = datos[datos["Grade"] == boton_tam_siz ]
    fig, ax =plt.subplots()
    ax.hist(dph["Tumor Size"],color = "pink", edgecolor = "white")
    ax.set_title(f"Grado {boton_tam_siz}")
    ax.set_xlabel("Tamaño")
    ax.set_ylabel("Personas")
    st.pyplot(fig)

if Menu == "Prueba":
    ts = datos["Grade"].unique()
    boton_tam_siz = st.sidebar.selectbox("Tamaño ", options = ts )
    xs = datos["Grade"]
    ys = datos["Tumor Size"]
    fig = px.scatter(x=(xs), y=(ys))
    st.plotly_chart(fig, use_container_width=True)

    
