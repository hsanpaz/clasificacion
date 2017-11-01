import numpy as np
import scipy.misc
from numpy import genfromtxt
class clasificacion(object):
    #constructor de la clase
    def __init__(self,nombre_imagen):
        self.nombre_imagen=nombre_imagen
        self.W1 = genfromtxt('pesos/W1.csv', delimiter=',') #primera capa de pesos de la red neuronal
        self.W2 = genfromtxt('pesos/W2.csv', delimiter=',') #segunda capa de pesos de la red neuronal
        self.W3 = genfromtxt('pesos/W3.csv', delimiter=',') #tercera capa de pesos de la red neuronal
        self.img = scipy.misc.imread("imag/"+ self.nombre_imagen)
        
    #obtiene los histogramas de una imagen a partir de una matriz RGB
    def obtener_histograma(self,imagen_RGB):
        rango = np.arange(257)#niveles de cada color 0 - 255
        R , XX = np.histogram(imagen_RGB[:,:,0],rango)#histograma para el color rojo
        R = R.astype(float)#conversion de entero a coma flotante
        R=R/max(R)# normalizacion de datos
        G , XX = np.histogram(imagen_RGB[:,:,1],rango)#histograma para el color verde
        G=G.astype(float)#conversion de entero a coma flotante
        G=G/max(G)# normalizacion de datos
        B , XX = np.histogram(imagen_RGB[:,:,2],rango)#histograma para el color azul
        B=B.astype(float)#conversion de entero a coma flotante
        B=B/max(B)# normalizacion de datos
        self.histograma = np.concatenate((R,G),axis=0) #concatenamos histogramas de rojo y verde
        self.histograma = np.concatenate((self.histograma,B),axis=0) #concatenamos histograma azul con los dos anteriores
        self.histograma = self.histograma.T
        self.histograma=np.insert(self.histograma,len(self.histograma),1) #extension para la red neuronal

    #Clasifica Una imagen a partir de du histograma RGB
    def red_neuronal(self,histograma):
        G= np.dot(histograma,self.W1)#paso por la capa 1
        G1=1/(1+np.exp(-G))#funcion de activacion de la capa1
        G1=np.insert(G1,len(G1),1)
        G = np.dot(G1,self.W2)#paso por la capa 2
        G2=1/(1+np.exp(-G))#funcion de activacion de la capa2
        G2=np.insert(G2,len(G2),1)
        G = np.dot(G2,self.W3)#paso por la capa 3
        self.Y=round(1/(1+np.exp(-G)))#funcion de activacion de la capa3
        print int(self.Y)#salida de la red neuronal


print "clasificacion  imagen de prueba rural: "
CLS = clasificacion("test1.jpg")
CLS.obtener_histograma(CLS.img)
CLS.red_neuronal(CLS.histograma)
