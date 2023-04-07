const express= require('express');
const fs= require('fs');
let bodyParser= require('body-parser');
let data= require('./data/person.json');
let myChesoi= require('./myGruppo.js');
const ejs= require('ejs');
const path= require('path');
const myGruppo= require('./myGruppo.js');
let app= express();

app.set("view engine", "ejs");
app.set("views", path.join(__dirname, "views"));
app.use(bodyParser.urlencoded({extended: false}));

app.get('/', function(req, res) {
  res.render('pages/index.ejs');
});

app.get('/post', (req, res) => {
  data = fs.readFileSync('./data/person.json', "utf8", (err, dati) => {
    if (err) {
      console.error(err);
      return;
    } else {
      return dati;
    }
  })
  res.render('pages/post.ejs', {data: JSON.parse(data)});
});

app.post('/scrivi', function(req, res) {
  let dataJSON= JSON.parse(fs.readFileSync('./data/person.json', 'utf8', function(err) {
    if(err){
      console.log(err);
    }
  }));

  let person = {
    username: req.body.username,
    description: req.body.description
  }

  myGruppo.AddElementToJSON(dataJSON, person)
  
  fs.writeFile('./data/person.json', JSON.stringify(dataJSON), (err) => {
    if (err) {
      throw err;
    }
    console.log('registrato nel file json');

  })
  res.redirect('post');
});

app.listen(8080)
