<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Psicología</title>
  <style>
    body {
      font-family: 'Segoe UI', Arial, sans-serif;
      background: #f7fafd;
      margin: 0;
      padding: 0;
    }
    .container {
      max-width: 900px;
      margin: 40px auto;
      background: #fff;
      border-radius: 18px;
      box-shadow: 0 6px 32px rgba(41,82,163,0.09);
      padding: 34px 22px;
    }
    h1 {
      text-align: center;
      color: #2952a3;
      margin-bottom: 20px;
      font-size: 2em;
      letter-spacing: 1px;
    }
    .semestre {
      margin-bottom: 22px;
      padding: 16px 14px 10px 14px;
      border-radius: 14px;
      box-shadow: 0 2px 14px #e3f0ff;
    }
    .semestre.rosado {
      background: linear-gradient(90deg, #ffd2eb 80%, #ffb6d5 100%);
    }
    .semestre.morado {
      background: linear-gradient(90deg, #e6d6ff 80%, #c7a6ff 100%);
    }
    .semestre.rojo {
      background: linear-gradient(90deg, #ffe5e5 80%, #ffb3b3 100%);
    }
    .semestre.azul {
      background: linear-gradient(90deg, #e3f0ff 80%, #b6d3ff 100%);
    }
    .sem-titulo {
      color: #fff;
      font-weight: bold;
      font-size: 1.14em;
      margin-bottom: 12px;
      letter-spacing: 0.5px;
      padding: 6px 18px;
      border-radius: 8px;
      box-shadow: 0 1px 6px rgba(41,82,163,0.08);
      display: inline-block;
    }
    .rosado .sem-titulo { background: #ff69b4; }
    .morado .sem-titulo { background: #8e44ad; }
    .rojo .sem-titulo { background: #e74c3c; }
    .azul .sem-titulo { background: #2980b9; }
    .ramo-list {
      list-style: none;
      padding: 0;
      margin-bottom: 0;
      margin-top: 10px;
      display: flex;
      flex-wrap: wrap;
      gap: 10px 22px;
    }
    .ramo-list li {
      min-width: 260px;
      margin-bottom: 10px;
      background: rgba(255,255,255,0.60);
      padding: 12px 18px;
      border-radius: 8px;
      display: flex;
      align-items: center;
      font-size: 1.09em;
      box-shadow: 0 1px 6px rgba(41,82,163,0.07);
      transition: background 0.25s;
    }
    .ramo-list input[type="checkbox"]:checked + label {
      color: #38761d;
      text-decoration: line-through;
      font-weight: bold;
    }
    .ramo-list input[type="checkbox"] {
      margin-right: 16px;
      accent-color: #2952a3;
      transform: scale(1.23);
    }
    .ramo-list input:disabled + label {
      color: #aaa;
      text-decoration: none;
    }
    @media (max-width: 600px) {
      .container { padding: 5vw 2vw; }
      .ramo-list li { min-width: 90vw; }
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>Psicología</h1>
    <div id="malla"></div>
  </div>
  <script>
    // Semestres y ramos exactos
    const semestres = [
      {nombre: "Primer semestre", clase: "rosado"},
      {nombre: "Segundo semestre", clase: "morado"},
      {nombre: "Tercer semestre", clase: "rojo"},
      {nombre: "Cuarto semestre", clase: "azul"}
    ];
    const asignaturas = [
      // Primer semestre
      { id: 'antropologia', nombre: 'Antropología', semestre: 0, prerrequisitos: [] },
      { id: 'fund_bio', nombre: 'Fundamentos Biológicos del Comportamiento Humano', semestre: 0, prerrequisitos: [] },
      { id: 'proc_cogn', nombre: 'Procesos Cognitivos', semestre: 0, prerrequisitos: [] },
      { id: 'evol_hist', nombre: 'Evolución Histórica de la Psicología', semestre: 0, prerrequisitos: [] },
      { id: 'fund_filo', nombre: 'Fundamentos Filosóficos de la Psicología', semestre: 0, prerrequisitos: [] },
      { id: 'taller_com', nombre: 'Taller de Comunicación', semestre: 0, prerrequisitos: [] },
      // Segundo semestre
      { id: 'etica', nombre: 'Ética', semestre: 1, prerrequisitos: ['antropologia'] },
      { id: 'neuropsic', nombre: 'Neuropsicología', semestre: 1, prerrequisitos: ['fund_bio'] },
      { id: 'fund_socant', nombre: 'Fundamentos Socioantropológicos del Comportamiento', semestre: 1, prerrequisitos: [] },
      { id: 'intro_metod', nombre: 'Introducción a la Metodología de la Investigación', semestre: 1, prerrequisitos: [] },
      { id: 'taller_grupal', nombre: 'Taller de Trabajo Grupal', semestre: 1, prerrequisitos: [] },
      { id: 'proc_afect', nombre: 'Procesos Afectivos', semestre: 1, prerrequisitos: [] },
      // Tercer semestre
      { id: 'electivo_int1', nombre: 'Electivo de Formación Integral 1', semestre: 2, prerrequisitos: ['etica'] },
      { id: 'psic_evol1', nombre: 'Psicología Evolutiva 1', semestre: 2, prerrequisitos: ['proc_cogn', 'proc_afect'] },
      { id: 'psic_personalidad', nombre: 'Psicología de la Personalidad', semestre: 2, prerrequisitos: ['proc_cogn', 'proc_afect'] },
      { id: 'psic_social1', nombre: 'Psicología Social 1', semestre: 2, prerrequisitos: [] },
      { id: 'metod_invest_psic', nombre: 'Metodología de la Investigación Aplicada a la Psicología', semestre: 2, prerrequisitos: ['intro_metod'] },
      { id: 'taller_entrevista', nombre: 'Taller de Entrevista', semestre: 2, prerrequisitos: [] },
      // Cuarto semestre
      { id: 'electivo_int2', nombre: 'Electivo de Formación Integral 2', semestre: 3, prerrequisitos: ['electivo_int1'] },
      { id: 'psicopat_general', nombre: 'Psicopatología General', semestre: 3, prerrequisitos: ['psic_personalidad'] },
      { id: 'psic_evol2', nombre: 'Psicología Evolutiva 2', semestre: 3, prerrequisitos: ['psic_evol1'] },
      { id: 'psic_social2', nombre: 'Psicología Social 2', semestre: 3, prerrequisitos: ['psic_social1'] },
      { id: 'analisis_datos_cuant', nombre: 'Análisis de Datos Cuantitativos', semestre: 3, prerrequisitos: ['metod_invest_psic'] },
      { id: 'eval_psic_cog', nombre: 'Evaluación Psicológica Cognitiva', semestre: 3, prerrequisitos: ['psic_personalidad', 'neuropsic'] }
    ];

    // Renderizado con color y sin mostrar prerrequisitos
    function render() {
      const mallaDiv = document.getElementById('malla');
      mallaDiv.innerHTML = '';
      semestres.forEach((sem, idx) => {
        const cont = document.createElement('div');
        cont.className = 'semestre ' + sem.clase;
        cont.innerHTML = `<span class="sem-titulo">${sem.nombre}</span>`;
        const ul = document.createElement('ul');
        ul.className = 'ramo-list';
        asignaturas.filter(a => a.semestre === idx).forEach(ramo => {
          const checked = localStorage.getItem(ramo.id) === '1';
          // Verifica si los prerrequisitos están marcados
          const habilitado = ramo.prerrequisitos.every(pr => localStorage.getItem(pr) === '1');
          const li = document.createElement('li');
          const input = document.createElement('input');
          input.type = 'checkbox';
          input.id = ramo.id;
          input.checked = checked;
          input.disabled = !habilitado;
          input.addEventListener('change', () => {
            localStorage.setItem(ramo.id, input.checked ? '1' : '0');
            render();
          });
          const label = document.createElement('label');
          label.htmlFor = ramo.id;
          label.textContent = ramo.nombre;
          li.appendChild(input);
          li.appendChild(label);
          ul.appendChild(li);
        });
        cont.appendChild(ul);
        mallaDiv.appendChild(cont);
      });
    }
    render();
  </script>
</body>
</html>
