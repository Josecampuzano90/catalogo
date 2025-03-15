using System;
using System.Collections.Generic;

class CatalogoRevistas
{
    static List<string> revistas = new List<string>()
    {
        "National Geographic", "Science", "Nature", "Time", "Forbes",
        "Popular Science", "The Economist", "Wired", "Scientific American", "Harvard Business Review"
    };

    static bool BusquedaRecursiva(List<string> lista, string titulo, int inicio, int fin)
    {
        if (inicio > fin) return false;
        int medio = (inicio + fin) / 2;
        if (lista[medio].Equals(titulo, StringComparison.OrdinalIgnoreCase)) return true;
        if (string.Compare(lista[medio], titulo, StringComparison.OrdinalIgnoreCase) > 0)
            return BusquedaRecursiva(lista, titulo, inicio, medio - 1);
        else
            return BusquedaRecursiva(lista, titulo, medio + 1, fin);
    }

    static bool BusquedaIterativa(List<string> lista, string titulo)
    {
        foreach (string revista in lista)
        {
            if (revista.Equals(titulo, StringComparison.OrdinalIgnoreCase))
                return true;
        }
        return false;
    }

    static void Main()
    {
        while (true)
        {
            Console.WriteLine("\nMenú:");
            Console.WriteLine("1. Buscar título (iterativo)");
            Console.WriteLine("2. Buscar título (recursivo)");
            Console.WriteLine("3. Salir");
            Console.Write("Seleccione una opción: ");
            
            string opcion = Console.ReadLine();
            if (opcion == "3") break;
            
            Console.Write("Ingrese el título a buscar: ");
            string titulo = Console.ReadLine();
            bool encontrado = false;
            
            if (opcion == "1")
                encontrado = BusquedaIterativa(revistas, titulo);
            else if (opcion == "2")
                encontrado = BusquedaRecursiva(revistas, titulo, 0, revistas.Count - 1);
            else
                Console.WriteLine("Opción no válida");
            
            Console.WriteLine(encontrado ? "Encontrado" : "No encontrado");
        }
    }
}
