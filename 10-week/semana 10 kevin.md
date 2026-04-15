import java.util.*;

public class Main {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);

        System.out.print("¿Cuántos estudiantes desea ingresar?: ");
        int cantidadEstudiante = scanner.nextInt();
        scanner.nextLine(); // limpiar buffer

        String[] tipoDocumento = new String[cantidadEstudiante];
        String[] documento = new String[cantidadEstudiante];
        String[] nombre = new String[cantidadEstudiante];
        String[] correo = new String[cantidadEstudiante];

        String[] tiposPermitidos = {"TI", "CC", "NIT"};
        String[] correosPermitidos = {"gmail.com", "hotmail.com", "outlook.com"};

        for (int i = 0; i < cantidadEstudiante; i++) {

            // -------- TIPO DE DOCUMENTO --------
            int pos;
            while (true) {
                System.out.println("\nSeleccione tipo de documento del estudiante " + (i + 1));
                for (int j = 0; j < tiposPermitidos.length; j++) {
                    System.out.println((j + 1) + ". " + tiposPermitidos[j]);
                }

                System.out.print("Opción: ");

                if (scanner.hasNextInt()) {
                    pos = scanner.nextInt();

                    if (pos >= 1 && pos <= tiposPermitidos.length) {
                        tipoDocumento[i] = tiposPermitidos[pos - 1];
                        break;
                    } else {
                        System.out.println("❌ Opción inválida.");
                    }
                } else {
                    System.out.println("❌ Solo números.");
                    scanner.next(); // limpiar
                }
            }

            scanner.nextLine(); // limpiar buffer

            // -------- DOCUMENTO --------
            while (true) {
                System.out.print("Ingrese número de documento: ");
                String docTemp = scanner.nextLine();

                if (!docTemp.matches("\\d+")) {
                    System.out.println("❌ Solo números permitidos.");
                    continue;
                }

                boolean repetido = false;
                for (int k = 0; k < i; k++) {
                    if (docTemp.equals(documento[k])) {
                        repetido = true;
                        System.out.println("❌ Documento repetido.");
                        break;
                    }
                }

                if (!repetido) {
                    documento[i] = docTemp;
                    break;
                }
            }

            // -------- NOMBRE --------
            while (true) {
                System.out.print("Ingrese nombre: ");
                String nombreTemp = scanner.nextLine();

                if (!nombreTemp.matches("[a-zA-ZáéíóúÁÉÍÓÚñÑ ]+")) {
                    System.out.println("❌ Solo letras.");
                    continue;
                }

                boolean repetido = false;
                for (int k = 0; k < i; k++) {
                    if (nombreTemp.equalsIgnoreCase(nombre[k])) {
                        repetido = true;
                        System.out.println("❌ Nombre repetido.");
                        break;
                    }
                }

                if (!repetido) {
                    nombre[i] = nombreTemp;
                    break;
                }
            }

            // -------- CORREO --------
            int correoPos;
            while (true) {
                System.out.println("Seleccione dominio del correo:");
                for (int j = 0; j < correosPermitidos.length; j++) {
                    System.out.println((j + 1) + ". " + correosPermitidos[j]);
                }

                System.out.print("Opción: ");

                if (scanner.hasNextInt()) {
                    correoPos = scanner.nextInt();

                    if (correoPos >= 1 && correoPos <= correosPermitidos.length) {
                        correoPos--; // ajustar índice
                        break;
                    } else {
                        System.out.println("❌ Opción inválida.");
                    }
                } else {
                    System.out.println("❌ Solo números.");
                    scanner.next();
                }
            }

            scanner.nextLine(); // limpiar buffer

            System.out.print("Ingrese usuario del correo: ");
            String usuarioCorreo = scanner.nextLine();

            correo[i] = usuarioCorreo + "@" + correosPermitidos[correoPos];

            System.out.println("✅ Estudiante registrado correctamente\n");
        }

        // -------- MOSTRAR DATOS --------
        System.out.println("\n===== LISTA DE ESTUDIANTES =====");
        for (int i = 0; i < cantidadEstudiante; i++) {
            System.out.println("Estudiante " + (i + 1));
            System.out.println("Tipo Doc: " + tipoDocumento[i]);
            System.out.println("Documento: " + documento[i]);
            System.out.println("Nombre: " + nombre[i]);
            System.out.println("Correo: " + correo[i]);
            System.out.println("---------------------------");
        }

        scanner.close();
    }
}