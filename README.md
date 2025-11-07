import numpy as np
import matplotlib.pyplot as plt

def make_autopct(values):
    def my_autopct(pct):
        total = np.sum(values)
        absolute = int(round(pct * total / 100.0))
        return "{:.1f}%\n({:d} g)".format(pct, absolute) if absolute > 0 else ""
    return my_autopct

data = np.array([300, 150, 200, 50])
cars = ["Ford", "BMW", "Fiat", "Audi"]
explode = (0.05, 0, 0, 0)
colors = plt.cm.Pastel1(np.linspace(0, 1, len(data)))
wp = dict(width=0.6, edgecolor='white')

fig, ax = plt.subplots(figsize=(10, 7))
wedges, texts, autotexts = ax.pie(
    data,
    autopct=make_autopct(data),
    explode=explode,
    labels=cars,
    shadow=True,
    colors=colors,
    startangle=90,
    wedgeprops=wp,
    textprops=dict(color="magenta"),
)

ax.legend(wedges, cars, title="Cars", loc="center left", bbox_to_anchor=(1, 0, 0.5, 1))
plt.setp(autotexts, size=8, weight="bold")
ax.set_title("Customizing pie chart")
plt.show()
