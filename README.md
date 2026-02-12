import express from "express";
import bodyParser from "body-parser";
import fetch from "node-fetch";

const app = express();
app.use(bodyParser.json());

app.post("/generar-ensayo", async (req, res) => {
  const { tema } = req.body;

  // Aquí llamas a la API de generación de texto
  const respuesta = await fetch("https://api.openai.com/v1/chat/completions", {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
      "Authorization": `Bearer TU_API_KEY`
    },
    body: JSON.stringify({
      model: "gpt-4",
      messages: [
 { role: "system", content: "Eres un generador de ensayos académicos." }, 
 { role: "user", content: `Escribe un ensayo sobre: ${tema}` }
      ]
    })
  });

  const data = await respuesta.json();
  res.json({ ensayo: data.choices[0].message.content });
});

app.listen(3000, () => console.log("Servidor en http://localhost:3000"));
