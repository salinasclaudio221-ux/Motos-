# Motos-
Venta De 0 km
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Motos Azul - Comercialización de Motos</title>
  <style>
    :root {
      --azul-oscuro: #003f7f;
      --azul: #0057B8;
      --azul-claro: #e0f0ff;
      --blanco: #ffffff;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      font-family: 'Segoe UI', sans-serif;
      background-color: var(--azul-claro);
      color: #333;
    }

    header {
      background-color: var(--azul);
      color: var(--blanco);
      padding: 30px 20px;
      text-align: center;
    }

    nav {
      background-color: var(--azul-oscuro);
      display: flex;
      justify-content: center;
      gap: 40px;
      padding: 12px;
    }

    nav a {
      color: white;
      text-decoration: none;
      font-weight: bold;
      transition: 0.3s;
    }

    nav a:hover {
      color: #ffd700;
    }

    .filtros {
      padding: 20px;
      background: #dcefff;
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      gap: 20px;
    }

    .filtros select {
      padding: 10px;
      border-radius: 5px;
      border: 1px solid #ccc;
      min-width: 180px;
    }

    .catalogo {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      padding: 20px;
      gap: 20px;
    }

    .moto {
      background: white;
      border: 1px solid #ccc;
      border-radius: 10px;
      width: 300px;
      padding: 15px;
      box-shadow: 0 2px 6px rgba(0,0,0,0.1);
    }

    .moto img {
      width: 100%;
      border-radius: 8px;
    }

    .btn {
      background-color: var(--azul);
      color: white;
      padding: 10px;
      border: none;
      border-radius: 5px;
      display: block;
      text-align: center;
      margin-top: 10px;
      text-decoration: none;
      cursor: pointer;
    }

    .btn:hover {
      background-color: #004a9f;
    }

    section#financiamiento {
      padding: 40px 20px;
      background-color: white;
      text-align: center;
    }

    #financiamiento input,
    #financiamiento select {
      padding: 10px;
      margin: 10px;
      width: 200px;
    }

    footer {
      background-color: var(--azul-oscuro);
      color: white;
      text-align: center;
      padding: 20px;
      margin-top: 40px;
    }

    @media (max-width: 768px) {
      .catalogo {
        flex-direction: column;
        align-items: center;
      }

      .filtros {
        flex-direction: column;
        align-items: center;
      }

      nav {
        flex-direction: column;
        gap: 10px;
      }
    }
  </style>
</head>
<body>

  <header>
    <h1>Motos Azul</h1>
    <p>Tu próxima moto está aquí. ¡Explora y financia fácilmente!</p>
  </header>

  <nav>
    <a href="#catalogo">Catálogo</a>
    <a href="#financiamiento">Financiamiento</a>
    <a href="#contacto">Contacto</a>
  </nav>

  <section class="filtros">
    <select id="marcaFiltro">
      <option value="">Todas las marcas</option>
      <option value="Yamaha">Yamaha</option>
      <option value="Honda">Honda</option>
      <option value="Suzuki">Suzuki</option>
    </select>

    <select id="tipoFiltro">
      <option value="">Todos los tipos</option>
      <option value="Deportiva">Deportiva</option>
      <option value="Urbana">Urbana</option>
      <option value="Adventure">Adventure</option>
    </select>

    <select id="precioFiltro">
      <option value="">Todos los precios</option>
      <option value="bajo">Menos de $5,000</option>
      <option value="medio">$5,000 - $8,000</option>
      <option value="alto">Más de $8,000</option>
    </select>
  </section>

  <section class="catalogo" id="catalogo">
    <!-- Las motos se generan con JS -->
  </section>

  <section id="financiamiento">
    <h2>Simulador de Financiamiento</h2>
    <p>Ingresa el valor de la moto y selecciona plazo:</p>
    <input type="number" id="monto" placeholder="Valor de la moto ($)" />
    <select id="cuotas">
      <option value="6">6 meses</option>
      <option value="12">12 meses</option>
      <option value="24">24 meses</option>
    </select>
    <br />
    <button class="btn" onclick="simular()">Calcular</button>
    <p id="resultado"></p>
  </section>

  <footer id="contacto">
    <p>&copy; 2025 Motos Azul | Contacto: contacto@motosazul.com</p>
  </footer>

  <script>
    const motos = [
      {
        nombre: "Yamaha MT-03",
        marca: "Yamaha",
        tipo: "Deportiva",
        precio: 5500,
        imagen: "https://via.placeholder.com/300x200?text=Yamaha+MT-03"
      },
      {
        nombre: "Honda CB 500F",
        marca: "Honda",
        tipo: "Urbana",
        precio: 6200,
        imagen: "https://via.placeholder.com/300x200?text=Honda+CB+500F"
      },
      {
        nombre: "Suzuki V-Strom 650",
        marca: "Suzuki",
        tipo: "Adventure",
        precio: 8500,
        imagen: "https://via.placeholder.com/300x200?text=Suzuki+V-Strom+650"
      },
      {
        nombre: "Honda CBR 500R",
        marca: "Honda",
        tipo: "Deportiva",
        precio: 7300,
        imagen: "https://via.placeholder.com/300x200?text=Honda+CBR+500R"
      }
    ];

    const catalogo = document.querySelector(".catalogo");

    function mostrarMotos(filtro = {}) {
      catalogo.innerHTML = "";
      const filtradas = motos.filter(moto => {
        return (!filtro.marca || moto.marca === filtro.marca) &&
               (!filtro.tipo || moto.tipo === filtro.tipo) &&
               (!filtro.precio || (
                 filtro.precio === "bajo" && moto.precio < 5000 ||
                 filtro.precio === "medio" && moto.precio >= 5000 && moto.precio <= 8000 ||
                 filtro.precio === "alto" && moto.precio > 8000
               ));
      });

      if (filtradas.length === 0) {
        catalogo.innerHTML = "<p>No se encontraron motos con esos filtros.</p>";
      } else {
        filtradas.forEach(moto => {
          catalogo.innerHTML += `
            <div class="moto">
              <img src="${moto.imagen}" alt="${moto.nombre}">
              <h3>${moto.nombre}</h3>
              <p>Marca: ${moto.marca}</p>
              <p>Tipo: ${moto.tipo}</p>
              <p>
              
