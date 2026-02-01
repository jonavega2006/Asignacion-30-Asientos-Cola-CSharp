using System;
using System.Collections.Generic;

namespace AsignacionAsientosCola
{
    // Clase Persona
    class Persona
    {
        public string Nombre { get; set; }
        public int NumeroAsiento { get; set; }

        public Persona(string nombre, int numeroAsiento)
        {
            Nombre = nombre;
            NumeroAsiento = numeroAsiento;
        }
    }

    // Clase que maneja la cola de asientos
    class SistemaAsientos
    {
        private Queue<Persona> cola;
        private int capacidadMaxima;
        private int asientoActual;

        public SistemaAsientos(int capacidad)
        {
            cola = new Queue<Persona>();
            capacidadMaxima = capacidad;
            asientoActual = 1;
        }

        public void RegistrarPersona()
        {
            if (cola.Count < capacidadMaxima)
            {
                Console.Write("Ingrese el nombre de la persona: ");
                string nombre = Console.ReadLine();

                Persona persona = new Persona(nombre, asientoActual);
                cola.Enqueue(persona);

                Console.WriteLine($"Asiento {asientoActual} asignado a {nombre}");
                asientoActual++;
            }
            else
            {
                Console.WriteLine("No hay asientos disponibles. La cola está llena.");
            }
        }

        public void MostrarAsientos()
        {
            Console.WriteLine("\n--- LISTA DE ASIENTOS ASIGNADOS ---");

            if (cola.Count == 0)
            {
                Console.WriteLine("No hay personas registradas.");
                return;
            }

            foreach (Persona p in cola)
            {
                Console.WriteLine($"Asiento {p.NumeroAsiento}: {p.Nombre}");
            }
        }
    }

    // Programa principal
    class Program
    {
        static void Main(string[] args)
        {
            SistemaAsientos sistema = new SistemaAsientos(30);
            int opcion;

            do
            {
                Console.WriteLine("\n=== ASIGNACIÓN DE 30 ASIENTOS (COLA) ===");
                Console.WriteLine("1. Registrar persona");
                Console.WriteLine("2. Mostrar asientos asignados");
                Console.WriteLine("3. Salir");
                Console.Write("Seleccione una opción: ");

                if (!int.TryParse(Console.ReadLine(), out opcion))
                {
                    Console.WriteLine("Ingrese un número válido.");
                    continue;
                }

                switch (opcion)
                {
                    case 1:
                        sistema.RegistrarPersona();
                        break;

                    case 2:
                        sistema.MostrarAsientos();
                        break;

                    case 3:
                        Console.WriteLine("Saliendo del sistema...");
                        break;

                    default:
                        Console.WriteLine("Opción inválida.");
                        break;
                }

            } while (opcion != 3);
        }
    }

