
Beim Environment-Mapping geht es darum Objekte mit reflektierender Oberfläche darzustellen.
Dementsprechend muss die Oberfläche eine Spiegelung der Umgebung sein.
Allerdings besteht diese Umgebung nicht aus geometrischen Repräsentationen, sonder ist ein gespeichertes Bild der Umgebung.

Beim Raytracing gilt: Trifft ein Strahl kein Objekte, dann wird das Licht des Strahl aus der Environment-Map ausgelesen.

Man kann sich eine Environment-Map also als eine Textur vorstellen, die auf einer virtuellen Kugel um ein Objekt, eine Szene gelegt wird.

Zur Vereinfachung betrachtet man nur die Richtung eines reflektierten Strahl, nicht aber seinen Ursprungspunkt.

## Parametrisierung
Es wird immer der Richtungsvektor $\vec{r}, |\vec{r}| = 1$ verwendet.

### Latitude/Longitude Maps
Parametrisierung über:
- Polarwinkel $\theta \in [0, \pi]$
- Azimuthalwinkel $\phi \in [0, 2\pi]$

Berechnungsvorschrift für den Zugriff auf eine Textur mit der Auflösung $s \times t$:
$$
	\left.
	\begin{aligned}
		\theta &= \arccos(\vec{r}_z)\\
		\phi &= \arctan_2(\vec{r}_y, \vec{r}_x)
	\end{aligned}
	\right\}
	\Rightarrow
	\begin{aligned}
		t &= \frac{\theta}{\pi}\\
		s &= \frac{\phi}{2\pi}
	\end{aligned}
$$
Nachteile:
- vergleichsweise teuere Berechnung der Texturkoordinate
- sehr ungleichmäßige Abtastung an den Polen (Nordpol, Südpol)



### Sphere Mapping

Beim Sphere-Mapping fotografiert man eine Spiegelkugel. Dieses Bild dient dann als Textur.
![](sphere_mapping.png)
Um diese Textur auslese zu können, muss man jedoch die Aufnachmerichtung kennen.

Nachteile:
- Die Abtastrate ist maximal für Richtungen entgegen der Aufnahmerichtung
- Die Abtastung ist nicht gleichmäßig, ungleichmäßig an den Rändern.
- Nur für Blickrichtungen ähnlich der Aufnahmerichtung geeignet.

### Cube Environment Maps

Bei Cube-Environment-Maps ist die Szene eingebettet in eine Würfel, an dem jede Seite eine 2D Textur der Umgebung ist.


### Aufnahmetechniken

In der Praxis verwendet man spiegelnde Chromkugeln, um die Umgebung aufzunehmen.
Außerdem macht man mehrere Aufnahmen um das Problem der ungleichmäßigen Abtastung zu beheben. 
Damit lässt sich auch die Kamera, die die Aufnahme macht aus der Environment Map entfernen.


### Vorfilterung

Bei imperfekter Spiegelung trägt Licht aus einem ganzen Bereich zur Spiegelung bei:
![[Vorfilterung_Environment_Maps.png]]

Um eine Environment-Map/Textur nicht mehrfach abtasten zu müssen, kann man sie stattdessen vorflitern, damm wird die gewichtete Summe über einen Winkelbereich gespeichert.