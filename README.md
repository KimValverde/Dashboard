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


Menu =st.sidebar.radio("Menu",["Inicio","Graficos", "Informacion"])
#1 boton
if Menu == "Inicio":
    st.title ("Introducción a la programación")
    st.header ("Proyecto 1")
    st.subheader ("Barrantes, G y Valverde, K")
    st.text("En la siguiente pagina podra buscar graficos con respecto al cancer de seno")
    st.text("a partir de un estudio realizado por SEER Program of the NCI en el 2017.")
    st.write("Para ver los datos originales [link](https://www.kaggle.com/datasets/reihanenamdari/breast-cancer)")
    st.text("INSTRUCCIONES: abra la pestaña al lado izquierdo y seleccione")
    st.text("en Menu la variable que quiere visualizar en el gráfico.")
    st.expander("imagen")
    st.image("imagen.jpg")
#2boton
if Menu == "Graficos":
    Graficos1 = ("Informacion de la poblacion estudiada", "Grado de cancer acorde la edad","Tamaño del tumor asociado al grado","Meses de supervivencia vs distintas variables", "Edad asociada a la diferenciacion")
    Menu = st.sidebar.selectbox("Tipo de Grafico", options = (Graficos1))

    if Menu == "Informacion de la poblacion estudiada":
        col1, col2 = st.columns(2)
        with col1:
            df = px.data.tips()
            n = datos["Race1"]
            v = datos["Race2"]
            fig = px.pie(df, values=(v), names=(n))
            st.plotly_chart(fig, use_container_width=True)
        with col2:
            df = px.data.tips()
            n = datos["Age1"]
            v = datos["Age2"]
            fig = px.pie(df, values=(v), names=(n))
            st.plotly_chart(fig, use_container_width=True)
            
        
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

    if Menu == "Meses de supervivencia vs distintas variables":
        col1, col2 = st.columns(2)
        with col1:
            xs = datos["Tumor Size"]
            ys = datos["Survival Months"]
            fig = px.scatter(x=(xs), y=(ys)).update_layout(yaxis={"title": "Meses de supervivencia"}, legend={"title":"column"})
            fig.update_layout(xaxis={"title": "Tamaño del tumor"}, legend={"title":"column"})
            st.plotly_chart(fig, use_container_width=True)
        with col2:
            xs = datos["Age"]
            ys = datos["Survival Months"]
            fig = px.scatter(x=(xs), y=(ys)).update_layout(yaxis={"title": "Meses de supervivencia"}, legend={"title":"column"})
            fig.update_layout(xaxis={"title": "Edad"}, legend={"title":"column"})
            st.plotly_chart(fig, use_container_width=True)

    if Menu == "Edad asociada a la diferenciacion":
        df = px.data.tips()
        value = datos["Race"]
        names = datos["Num"]
        fig = px.pie(df, values=(value), names=(names))
        st.plotly_chart(fig, use_container_width=True)

#3 boton
if Menu== "Informacion":
    Graficos1 = ("Testimonios", "Recomendaciones","Otros articulos relacionados",)
    Menu = st.sidebar.selectbox("Tipo de Grafico", options = (Graficos1))
    if Menu == "Testimonios":
        st.title ("Testimonios de pacientes con Cancer")
    if Menu == "Recomendaciones":
        st.title ("Recomendaciones")
    if Menu == "Otros articulos":
        st.title ("Poner links")
        

## grafico pie
    #df = px.data.tips()
    #value = datos["Race"]
    #names = datos["Num"]
    #fig = px.pie(df, values=(value), names=(names))
    #st.plotly_chart(fig, use_container_width=True)
## pestañas
    #ayuda para mas informacion de como ayudar a a una persona
    # personas que se han recuperado y como evitar caer de nuevo
