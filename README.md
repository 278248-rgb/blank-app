import streamlit as st
import numpy as np
import matplotlib.pyplot as plt

# Funkce pro výpočet bodů na kruhu
def generate_circle_points(center, radius, num_points):
    # Generování úhlů pro rovnoměrně rozložené body na kruhu
    angles = np.linspace(0, 2 * np.pi, num_points, endpoint=False)
    x_points = center[0] + radius * np.cos(angles)
    y_points = center[1] + radius * np.sin(angles)
    return x_points, y_points

# Streamlit aplikace
def main():
    # Název aplikace
    st.title('Kruhová Distribuce Bodů')

    # Vstupy pro střed, poloměr a počet bodů
    st.header('Nastavení')
    center_x = st.number_input('X-ová souřadnice středu', value=0)
    center_y = st.number_input('Y-ová souřadnice středu', value=0)
    radius = st.number_input('Poloměr', min_value=1, value=5)
    num_points = st.slider('Počet bodů', min_value=3, max_value=100, value=20)
    color = st.color_picker('Vyber barvu bodů', '#00f900')

    # Generování bodů na kruhu
    x_points, y_points = generate_circle_points((center_x, center_y), radius, num_points)

    # Vykreslení grafu
    fig, ax = plt.subplots()
    ax.scatter(x_points, y_points, color=color)
    ax.set_aspect('equal')
    ax.set_xlabel('X')
    ax.set_ylabel('Y')
    ax.set_title(f'Kruhová distribuce bodů (poloměr {radius})')

    # Zobrazení grafu
    st.pyplot(fig)

if __name__ == '__main__':
    main()
