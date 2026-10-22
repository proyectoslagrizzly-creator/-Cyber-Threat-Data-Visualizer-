# -Cyber-Threat-Data-Visualizer-
Una herramienta de análisis y visualización de datos desarrollada en **Python**. Este script simula la ingesta de logs de un Firewall o un sistema de detección de intrusos (IDS) y genera gráficos estadísticos automáticos para identificar tendencias de ataques informáticos.  
import matplotlib.pyplot as plt
import collections

class SecurityDataVisualizer:
    def __init__(self, log_data):
        self.log_data = log_data

    def process_data(self):
        # Cuenta la frecuencia de cada tipo de ataque
        return dict(collections.Counter(self.log_data))

    def generate_bar_chart(self, filename="grafica_amenazas.png"):
        data_count = self.process_data()
        
        # Separar categorías y valores
        threats = list(data_count.keys())
        counts = list(data_count.values())

        # Configuración de la gráfica
        plt.figure(figsize=(10, 6))
        colors = ['#e63946', '#f4a261', '#2a9d8f', '#264653', '#e9c46a']
        
        bars = plt.bar(threats, counts, color=colors[:len(threats)])
        
        # Diseño y etiquetas
        plt.title('Análisis de Amenazas de Red Detectadas', fontsize=16, fontweight='bold')
        plt.xlabel('Vector de Ataque', fontsize=12)
        plt.ylabel('Intentos Bloqueados', fontsize=12)
        plt.grid(axis='y', linestyle='--', alpha=0.7)

        # Añadir el número exacto sobre cada barra
        for bar in bars:
            yval = bar.get_height()
            plt.text(bar.get_x() + bar.get_width()/2, yval + 0.2, int(yval), ha='center', va='bottom', fontweight='bold')

        # Guardar y mostrar
        plt.savefig(filename, dpi=300, bbox_inches='tight')
        print(f"¡Análisis completado! Gráfica guardada como '{filename}'.")
        plt.show()

if __name__ == "__main__":
    # Logs simulados de un firewall
    firewall_logs = [
        "DDoS", "Phishing", "SQL Injection", "DDoS", "Fuerza Bruta",
        "Phishing", "Phishing", "DDoS", "Malware", "Malware",
        "SQL Injection", "Fuerza Bruta", "Malware", "DDoS", "DDoS"
    ]

    print("Iniciando análisis de telemetría de red...")
    visualizer = SecurityDataVisualizer(firewall_logs)
    visualizer.generate_bar_chart()
