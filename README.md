# index.html
I'll create a complete second-hand vehicle marketplace website with buyer verification features and seller listing capabilities. Here's the full code:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AutoCheck - Verified Second Hand Vehicles</title>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            line-height: 1.6;
            color: #333;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 20px;
        }

        /* Header */
        header {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 1rem 0;
            position: fixed;
            width: 100%;
            top: 0;
            z-index: 1000;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }

        nav {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .logo {
            font-size: 1.8rem;
            font-weight: bold;
        }

        .nav-links {
            display: flex;
            list-style: none;
            gap: 2rem;
        }

        .nav-links a {
            color: white;
            text-decoration: none;
            transition: opacity 0.3s;
        }

        .nav-links a:hover {
            opacity: 0.8;
        }

        .auth-buttons {
            display: flex;
            gap: 1rem;
        }

        .btn {
            padding: 0.7rem 1.5rem;
            border: none;
            border-radius: 25px;
            cursor: pointer;
            font-weight: 500;
            transition: all 0.3s;
            text-decoration: none;
            display: inline-block;
        }

        .btn-primary {
            background: #ff6b6b;
            color: white;
        }

        .btn-primary:hover {
            background: #ff5252;
            transform: translateY(-2px);
        }

        .btn-secondary {
            background: transparent;
            color: white;
            border: 2px solid white;
        }

        .btn-secondary:hover {
            background: white;
            color: #667eea;
        }

        /* Main Content */
        main {
            margin-top: 80px;
        }

        .hero {
            background: linear-gradient(rgba(0,0,0,0.5), rgba(0,0,0,0.5)), url('data:image/svg+xml,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1200 600"><rect fill="%23667eea" width="1200" height="600"/><circle fill="%23ff6b6b" opacity="0.3" cx="200" cy="200" r="100"/><circle fill="%23764ba2" opacity="0.2" cx="1000" cy="400" r="150"/></svg>');
            background-size: cover;
            color: white;
            text-align: center;
            padding: 4rem 0;
        }

        .hero h1 {
            font-size: 3rem;
            margin-bottom: 1rem;
        }

        .hero p {
            font-size: 1.2rem;
            margin-bottom: 2rem;
            max-width: 600px;
            margin-left: auto;
            margin-right: auto;
        }

        /* Vehicle Cards */
        .vehicles-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
            gap: 2rem;
            padding: 3rem 0;
        }

        .vehicle-card {
            background: white;
            border-radius: 15px;
            overflow: hidden;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
            transition: transform 0.3s, box-shadow 0.3s;
            cursor: pointer;
        }

        .vehicle-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 20px 40px rgba(0,0,0,0.15);
        }

        .vehicle-image {
            height: 200px;
            background: linear-gradient(45deg, #f0f0f0, #e0e0e0);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 4rem;
            color: #999;
        }

        .vehicle-info {
            padding: 1.5rem;
        }

        .vehicle-title {
            font-size: 1.3rem;
            font-weight: bold;
            margin-bottom: 0.5rem;
            color: #333;
        }

        .vehicle-price {
            font-size: 1.5rem;
            font-weight: bold;
            color: #ff6b6b;
            margin-bottom: 1rem;
        }

        .vehicle-stats {
            display: flex;
            justify-content: space-between;
            margin-bottom: 1rem;
            font-size: 0.9rem;
            color: #666;
        }

        .condition-badge {
            display: inline-block;
            padding: 0.3rem 0.8rem;
            border-radius: 20px;
            font-size: 0.8rem;
            font-weight: 500;
        }

        .condition-excellent { background: #4caf50; color: white; }
        .condition-good { background: #ff9800; color: white; }
        .condition-fair { background: #f44336; color: white; }

        .vehicle-actions {
            display: flex;
            gap: 0.5rem;
            margin-top: 1rem;
        }

        /* Modal */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.8);
            z-index: 2000;
            backdrop-filter: blur(5px);
        }

        .modal-content {
            background: white;
            margin: 5% auto;
            padding: 2rem;
            width: 90%;
            max-width: 800px;
            border-radius: 15px;
            max-height: 90vh;
            overflow-y: auto;
        }

        .close {
            float: right;
            font-size: 2rem;
            cursor: pointer;
            color: #999;
        }

        .close:hover {
            color: #333;
        }

        .report-section {
            background: #f8f9fa;
            padding: 1.5rem;
            border-radius: 10px;
            margin: 1rem 0;
        }

        .report-item {
            display: flex;
            justify-content: space-between;
            margin-bottom: 0.8rem;
            padding-bottom: 0.8rem;
            border-bottom: 1px solid #eee;
        }

        .report-item:last-child {
            border-bottom: none;
            margin-bottom: 0;
        }

        .cost-estimate {
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            padding: 1.5rem;
            border-radius: 10px;
            margin-top: 1.5rem;
        }

        /* Form Styles */
        .form-group {
            margin-bottom: 1.5rem;
        }

        .form-group label {
            display: block;
            margin-bottom: 0.5rem;
            font-weight: 500;
            color: #333;
        }

        .form-group input,
        .form-group select,
        .form-group textarea {
            width: 100%;
            padding: 0.8rem;
            border: 2px solid #e0e0e0;
            border-radius: 8px;
            font-size: 1rem;
            transition: border-color 0.3s;
        }

        .form-group input:focus,
        .form-group select:focus,
        .form-group textarea:focus {
            outline: none;
            border-color: #667eea;
        }

        /* Seller Dashboard */
        .dashboard {
            padding: 3rem 0;
        }

        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 2rem;
            margin-bottom: 3rem;
        }

        .stat-card {
            background: white;
            padding: 2rem;
            border-radius: 15px;
            text-align: center;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
        }

        .stat-number {
            font-size: 2.5rem;
            font-weight: bold;
            color: #ff6b6b;
        }

        /* Responsive */
        @media (max-width: 768px) {
            .nav-links {
                display: none;
            }

            .hero h1 {
                font-size: 2rem;
            }

            .vehicles-grid {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <!-- Header -->
    <header>
        <nav class="container">
            <div class="logo">
                <i class="fas fa-car"></i> AutoCheck
            </div>
            <ul class="nav-links">
                <li><a href="#home">Home</a></li>
                <li><a href="#vehicles">Vehicles</a></li>
                <li><a href="#seller">Sell</a></li>
            </ul>
            <div class="auth-buttons">
                <a href="#" class="btn btn-secondary" onclick="showLogin()">Login</a>
                <a href="#" class="btn btn-primary" onclick="showRegister()">Sign Up</a>
            </div>
        </nav>
    </header>

    <main>
        <!-- Hero Section -->
        <section class="hero" id="home">
            <div class="container">
                <h1>Buy Verified Second-Hand Vehicles</h1>
                <p>Get complete vehicle history, condition reports, and future maintenance cost estimates before you buy. No surprises, just transparency.</p>
                <a href="#vehicles" class="btn btn-primary" style="font-size: 1.1rem;">Browse Vehicles</a>
            </div>
        </section>

        <!-- Vehicles Section -->
        <section class="container" id="vehicles">
            <h2 style="text-align: center; margin: 3rem 0 2rem 0; font-size: 2.5rem;">Available Vehicles</h2>
            <div class="vehicles-grid" id="vehiclesGrid">
                <!-- Vehicles will be populated by JavaScript -->
            </div>
        </section>

        <!-- Seller Section -->
        <section class="dashboard container" id="seller" style="display: none;">
            <h2 style="text-align: center; margin-bottom: 2rem;">Seller Dashboard</h2>
            <div class="stats-grid">
                <div class="stat-card">
                    <div class="stat-number" id="viewsCount">0</div>
                    <div>Views</div>
                </div>
                <div class="stat-card">
                    <div class="stat-number" id="inquiriesCount">0</div>
                    <div>Inquiries</div>
                </div>
                <div class="stat-card">
                    <div class="stat-number" id="listingsCount">0</div>
                    <div>Listings</div>
                </div>
            </div>
            <button class="btn btn-primary" onclick="showListForm()" style="display: block; margin: 0 auto 2rem;">+ List New Vehicle</button>
            <div id="myListings"></div>
        </section>
    </main>

    <!-- Vehicle Details Modal -->
    <div id="vehicleModal" class="modal">
        <div class="modal-content">
            <span class="close" onclick="closeModal()">&times;</span>
            <div id="modalBody"></div>
        </div>
    </div>

    <!-- List Vehicle Form Modal -->
    <div id="listModal" class="modal">
        <div class="modal-content">
            <span class="close" onclick="closeListModal()">&times;</span>
            <h2>List Your Vehicle</h2>
            <form id="listForm">
                <div class="form-group">
                    <label>Vehicle Type</label>
                    <select id="vehicleType" required>
                        <option value="">Select Type</option>
                        <option value="car">Car</option>
                        <option value="bike">Bike</option>
                    </select>
                </div>
                <div class="form-group">
                    <label>Make & Model</label>
                    <input type="text" id="makeModel" placeholder="e.g., Toyota Corolla" required>
                </div>
                <div class="form-group">
                    <label>Year</label>
                    <input type="number" id="year" min="1990" max="2024" required>
                </div>
                <div class="form-group">
                    <label>Price (₹)</label>
                    <input type="number" id="price" required>
                </div>
                <div class="form-group">
                    <label>Mileage (km)</label>
                    <input type="number" id="mileage" required>
                </div>
                <div class="form-group">
                    <label>Condition</label>
                    <select id="condition" required>
                        <option value="">Select Condition</option>
                        <option value="excellent">Excellent</option>
                        <option value="good">Good</option>
                        <option value="fair">Fair</option>
                    </select>
                </div>
                <div class="form-group">
                    <label>Registration Number</label>
                    <input type="text" id="regNumber" required>
                </div>
                <div class="form-group">
                    <label>Accident History</label>
                    <select id="accidentHistory" required>
                        <option value="">Select</option>
                        <option value="none">No Accidents</option>
                        <option value="minor">Minor (1-2)</option>
                        <option value="major">Major (3+)</option>
                    </select>
                </div>
                <div class="form-group">
                    <label>Service History</label>
                    <select id="serviceHistory" required>
                        <option value="">Select</option>
                        <option value="complete">Complete Records</option>
                        <option value="partial">Partial Records</option>
                        <option value="none">No Records</option>
                    </select>
                </div>
                <div class="form-group">
                    <label>Description</label>
                    <textarea id="description" rows="4" placeholder="Additional details..."></textarea>
                </div>
                <button type="submit" class="btn btn-primary" style="width: 100%;">List Vehicle</button>
            </form>
        </div>
    </div>

    <script>
        // Sample data
        let vehicles = [];
        let currentUser = null;
        let userListings = [];

        // Initialize
        document.addEventListener('DOMContentLoaded', function() {
            loadSampleVehicles();
            updateVehiclesGrid();
        });

        // Sample vehicles data
        function loadSampleVehicles() {
            vehicles = [
                {
                    id: 1,
                    type: 'car',
                    makeModel: 'Toyota Corolla 2020',
                    year: 2020,
                    price: 850000,
                    mileage: 45000,
                    condition: 'excellent',
                    regNumber: 'DL01AB1234',
                    accidentHistory: 'none',
                    serviceHistory: 'complete',
                    description: 'Well maintained, single owner',
                    futureMaintenance: 25000,
                    conditionScore: 95
                },
                {
                    id: 2,
                    type: 'bike',
                    makeModel: 'Royal Enfield Classic 350',
                    year: 2022,
                    price: 185000,
                    mileage: 12000,
                    condition: 'excellent',
                    regNumber: 'MH02CD5678',
                    accidentHistory: 'none',
                    serviceHistory: 'complete',
                    description: 'Low mileage, garage kept',
                    futureMaintenance: 8000,
                    conditionScore: 98
                },
                {
                    id: 3,
                    type: 'car',
                    makeModel: 'Honda City 2018',
                    year: 2018,
                    price: 650000,
                    mileage: 78000,
                    condition: 'good',
                    regNumber: 'KA03EF9012',
                    accidentHistory: 'minor',
                    serviceHistory: 'partial',
                    description: 'Reliable daily driver',
                    futureMaintenance: 35000,
                    conditionScore: 85
                }
            ];
        }

        // Update vehicles grid
        function updateVehiclesGrid() {
            const grid = document.getElementById('vehiclesGrid');
            grid.innerHTML = vehicles.map(vehicle => createVehicleCard(vehicle)).join('');
        }

        // Create vehicle card
        function createVehicleCard(vehicle) {
            const conditionClass = `condition-${vehicle.condition}`;
            return `
                <div class="vehicle-card" onclick="showVehicleDetails(${vehicle.id})">
                    <div class="vehicle-image">
                        <i class="fas ${vehicle.type === 'car' ? 'fa-car' : 'fa-motorcycle'}"></i>
                    </div>
                    <div class="vehicle-info">
                        <div class="vehicle-title">${vehicle.makeModel}</div>
                        <div class="vehicle-price">₹${vehicle.price.toLocaleString()}</div>
                        <div class="vehicle-stats">
                            <span>${vehicle.year} • ${vehicle.mileage.toLocaleString()} km</span>
                            <span class="condition-badge ${conditionClass}">${vehicle.condition.toUpperCase()}</span>
                        </div>
                        <div style="margin-top: 1rem; color: #666; font-size: 0.9rem;">
                            ${vehicle.type === 'car' ? 'Car' : 'Bike'} • ${vehicle.regNumber}
                        </div>
                        <div class="vehicle-actions">
                            <i class="fas fa-chart-line" title="Condition Score: ${vehicle.conditionScore}%"></i>
                            <i class="fas fa-tools"
