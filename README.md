# PRACTICO
const  int buzzer=12;  // constante que contiene el número del pin de arduino al cual conectamos un buzzer                                                                                                                                                                                                                                      
 const int frecuencia[]={261,277,294,311,330,349,370,392,415,440,466,494};  // arreglo que contiene las frecuencias
 const int numFrecu=10;
 int laser=13;

void setup() 
{
  Serial.begin(9600); //transmisión de datos en serie. (9600) medición en baudios, muestra el resultado de la medición
  pinMode(buzzer, OUTPUT);
  pinMode(laser,OUTPUT);
  digitalWrite(buzzer,LOW);
  digitalWrite(laser,LOW);
  
}


void loop()
{
             int nivel=analogRead(A2); //debido a que es una medición análoga, el pin de entrada debe ser análoga
              Serial.print("EL NIVEL DEL RECIPIENTE ES:   ");
              Serial.println(nivel);
              delay(1000);

            
            int turbidez=analogRead(A0); // lee la entrada analógica del pin A0
           float volt= turbidez*(5.0/1024.0)*3;//la lectura análoga arrojada por el sensor va de 0 a 1023, podemos llevarla a una tensión de 0 a 5v
             int  NTU = -1120.4*square(volt)+5742.3*volt-4352.9;
            Serial. print("Valor del Sensor de Turbidez:        ");
            Serial.println(NTU);
            Serial. print ("Valor del voltaje:      ");
            Serial.println(volt);
            delay(200);   

              
    
    
          if (NTU < 1000) {
            Serial.println("  AGUA POTABLE "); 
            digitalWrite(buzzer,HIGH);
            delay(500);
            digitalWrite(buzzer,LOW);                                                                                                                                                
            delay(500);
            for(int i=0; i<numFrecu;i++)
              tone(buzzer,frecuencia[i]);
              delay(1000);
            noTone(buzzer); 
           }
           
          else if (NTU > 1000){                                                                                                                                                      
              Serial.println("   AGUA TURBIA   ");
              digitalWrite(laser,HIGH);
              delay(500);
              digitalWrite(laser, LOW);
              delay(500);
              digitalWrite(laser,HIGH);
              delay(500);
              digitalWrite(laser, LOW);
              delay(500);
             }
}
