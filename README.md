# Cloud-Computing


# Modul Praktikum 02 - Membuat API Sederhana dengan Flask


1. Masuk ke folder backend:
   ```bash
   cd cloud-project/backend
   ```
2. Membuat virtual environment:

    ```bash
    python -m venv venv
    ```

3. Aktivasi virtual environment:

    Untuk Windows:
    ```bash
    venv\Scripts\activate
    ```

4. Menginstal Flask
Instal Flask:
    ```bash
    pip install Flask
    ```


5. Menjalankan Aplikasi Flask
Jalankan aplikasi Flask:
    ```bash
    python app.py
    ```
6. Akses aplikasi flash di browser
    ```bash
    http://127.0.0.1:5000/
    http://localhost:5000/
    ```

# Modul Praktikum 03 - Membuat Aplikasi Frontend Sederhana dengan React + Vite

1. Berpindah ke direktori Frontend serta membuat proyek React baru dengan perintah
    ```bash
    cd frontend
    npm create vite@latest my-react-app -- --template react
    ```

2. Menjalankan React dan Vite menggunakan perintah
    ```bash
    npm run dev
    ```    

3. Membuat halaman sederhana pada src/App dengan code
    ```bash
    import React from 'react';

    function App() {
    return (
        <div style={{ textAlign: 'center', marginTop: '50px' }}>
        <h1>Hello from React + Vite!</h1>
        <p>This is a simple React app built with Vite.</p>
        </div>
    );
    }

    export default App;
    ```
4. Hasil tampilan jika dilihat pada browser
   <img src="asset/hasil prak 3.png" alt="Tampilan Aplikasi" width="700px">

# Modul Praktikum 04 - Menghubungkan React ke Flask

1. Menambahkan Endpoint pada Flask <br>
    Pada direktori backend/app.py tambahkan code sebagai berikut
    ```bash
    @app.route('/api/data')
    def get_data():
        return jsonify({"data": "Hello from Flask API"})
    ```
    Sehingga code fullnya seperti 
    ```bash
    from flask import Flask, jsonify

    app = Flask(__name__)

    @app.route('/')
    def home():
        return jsonify({"message": "Hello from Flask!"})

    @app.route('/api/data')
    def get_data():
        return jsonify({"data": "Hello from Flask API"})

    if __name__ == '__main__':
        app.run(debug=True, host='0.0.0.0', port=5000)
    ```
2. Menjalankan Flask dengan cara, pada terminal jalankan
    ```bash
    .\venv\Scripts\activate
    python app.py
    ```
    Kemudian buka browser dengan url
    ```bash
    http://localhost:5000/api/data
    ```

3. Memanggil Endpoint dari React <br>
    Pada file dengan direktori my-react-app/src/App.Jsx tambahkan code sebagai berikut
    ```bash
    import React, { useState, useEffect } from 'react';

    function App() {
    const [apiData, setApiData] = useState(null);

    useEffect(() => {
        fetch('http://localhost:5000/api/data')
        .then(response => response.json())
        .then(data => {
            setApiData(data.data);
        })
        .catch(error => console.error(error));
    }, []);

    return (
        <div style={{ textAlign: 'center', marginTop: '50px' }}>
        <h1>React & Flask Integration</h1>
        <p>{apiData ? apiData : "Loading data..."}</p>
        </div>
    );
    }

    export default App;
    ```
4. Menjalankan Aplikasi React
    Pada terminal jalankan
    ```bash
    npm run dev
    ```
    sehingga pada browser menampilkan
   <img src="asset/hasil prak 3.png" alt="Tampilan Aplikasi" width="700px">

5. Jika pada tampilan browser tidak menampilkan data dari Flask, maka tambahkan 
    - Install Flask-Cors
    ```bash
    pip install flask-cors
    ```
    - Tambahkan code di app.y
    ```bash
    from flask_cors import CORS
    CORS(app)
    ```
