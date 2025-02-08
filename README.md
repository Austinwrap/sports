<html lang="en">
<head>
  <meta charset="UTF-8">
  <!-- Ensure proper scaling on mobile devices -->
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Sports Stock Market Simulator</title>
  <style>
    /* ---------- Global Styles & Animated Background ---------- */
    body {
      margin: 0;
      padding: 0;
      background: linear-gradient(45deg, #000, #222, #000);
      background-size: 600% 600%;
      animation: gradientFlash 20s ease infinite;
      color: #fff;
      font-family: Arial, sans-serif;
    }
    @keyframes gradientFlash {
      0% { background-position: 0% 50%; }
      50% { background-position: 100% 50%; }
      100% { background-position: 0% 50%; }
    }
    /* ---------- Header, Tickers & Navigation ---------- */
    #header {
      position: fixed;
      top: 0;
      width: 100%;
      background: linear-gradient(45deg, #111, #222, #111);
      padding: 5px 0;
      border-bottom: 2px solid #28a745;
      z-index: 100;
    }
    /* Two ticker lines at the top; faster scrolling (7s) */
    #global-ticker, #extra-ticker {
      white-space: nowrap;
      overflow: hidden;
      font-size: 1em;
    }
    #global-ticker p, #extra-ticker p {
      display: inline-block;
      padding-left: 100%;
      animation: ticker 7s linear infinite;
    }
    @keyframes ticker {
      0% { transform: translateX(0); }
      100% { transform: translateX(-100%); }
    }
    #nav {
      text-align: center;
      margin-top: 5px;
    }
    #nav button {
      background-color: #28a745;
      border: none;
      color: #fff;
      padding: 8px 16px;
      margin: 5px;
      font-size: 1em;
      border-radius: 5px;
      cursor: pointer;
      box-shadow: 0 0 5px #28a745;
    }
    /* ---------- Main Content & Page Sections ---------- */
    #content {
      padding: 130px 20px 20px 20px; /* leave space for header and tickers */
    }
    .page { display: none; }
    .page.active { display: block; }
    /* ---------- Dashboard Styles ---------- */
    #dashboard { text-align: center; }
    #dashboard h1 { font-size: 2em; margin-bottom: 10px; }
    #balance-display { font-size: 1.5em; margin-bottom: 10px; }
    /* Portfolio Table with alternating row colors for clarity */
    #portfolio-table {
      margin: 0 auto;
      border-collapse: collapse;
      width: 90%;
      background-color: rgba(0, 0, 0, 0.8);
      color: #fff;
    }
    #portfolio-table th, #portfolio-table td {
      border: 1px solid #28a745;
      padding: 8px;
      text-align: center;
    }
    #portfolio-table tr:nth-child(even) {
      background-color: rgba(255,255,255,0.1);
    }
    /* ---------- Live Games Styles ---------- */
    #liveGame { text-align: center; }
    #live-games-container {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      gap: 15px;
      margin-top: 10px;
    }
    .live-game-event {
      background: rgba(255,255,255,0.1);
      border: 1px solid #28a745;
      border-radius: 5px;
      padding: 10px;
      width: 280px;
      text-align: left;
    }
    .live-game-event input {
      width: 70px;
      padding: 4px;
    }
    .live-game-event button {
      padding: 4px 8px;
      font-size: 0.9em;
      margin-left: 5px;
      cursor: pointer;
    }
    /* ---------- Stock Market Styles ---------- */
    #stockMarket table {
      width: 100%;
      border-collapse: collapse;
      background-color: rgba(0,0,0,0.8);
      color: #fff;
    }
    #stockMarket th, #stockMarket td {
      border: 1px solid #28a745;
      padding: 8px;
      text-align: center;
    }
    #stockMarket th { background-color: #333; }
    /* Make the team name (2nd column) appear in contrasting yellow */
    #stocks-body td:nth-child(2) {
      color: #ffcc00;
    }
    /* ---------- News Page Styles ---------- */
    #news { max-width: 800px; margin: 0 auto; }
    #news h1 { text-align: center; margin-bottom: 10px; }
    #news-container {
      border: 2px solid #28a745;
      padding: 10px;
      height: 300px;
      overflow-y: scroll;
      background: rgba(0,0,0,0.8);
      color: #fff;
    }
    .news-item { border-bottom: 1px solid #28a745; padding: 5px 0; font-size: 1em; }
    /* ---------- Instructions Page Styles ---------- */
    #instructions { max-width: 800px; margin: 0 auto; text-align: left; line-height: 1.6; }
    /* ---------- Cash Out / Celebration Page ---------- */
    #cashOut { text-align: center; font-size: 1.5em; }
    #cashOut button {
      padding: 10px 20px;
      font-size: 1em;
      margin-top: 20px;
      cursor: pointer;
    }
    /* ---------- Bottom Ticker ---------- */
    #bottom-ticker {
      position: fixed;
      bottom: 0;
      width: 100%;
      background: #111;
      padding: 5px 0;
      border-top: 2px solid #28a745;
      text-align: center;
      color: #0f0;
      white-space: nowrap;
      overflow: hidden;
      z-index: 100;
    }
    /* Faster bottom ticker: 5s duration */
    #bottom-ticker p {
      display: inline-block;
      padding-left: 100%;
      animation: ticker 5s linear infinite;
    }
    /* ---------- Confetti Container ---------- */
    #confetti-container {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      pointer-events: none;
      z-index: 200;
    }
    /* ---------- Neon Borders & Glows ---------- */
    table, #game-container, #news-container {
      border: 2px solid #28a745;
      box-shadow: 0 0 10px #28a745;
    }
    /* ---------- Responsive Styles for Mobile ---------- */
    @media (max-width: 600px) {
      body { font-size: 14px; }
      #nav button { padding: 6px 12px; font-size: 0.9em; }
      #portfolio-table, #stockMarket table { font-size: 0.8em; }
      #live-games-container, .live-game-event { width: 90%; }
      #global-ticker, #extra-ticker, #bottom-ticker { font-size: 0.9em; }
    }
  </style>
</head>
<body>
  <!-- HEADER: Tickers & Navigation -->
  <div id="header">
    <div id="global-ticker">
      <p id="ticker-text"></p>
    </div>
    <div id="extra-ticker">
      <p id="ticker-text-extra">Welcome to the Crazy Sports Market!</p>
    </div>
    <div id="nav">
      <button onclick="showSection('dashboard')">Dashboard</button>
      <button onclick="showSection('liveGame')">Live Games</button>
      <button onclick="showSection('stockMarket')">Stock Market</button>
      <button onclick="showSection('news')">News</button>
      <button onclick="showSection('instructions')">Instructions</button>
    </div>
  </div>
  
  <!-- MAIN CONTENT AREA -->
  <div id="content">
    <!-- Dashboard Page -->
    <div id="dashboard" class="page active">
      <h1>Dashboard</h1>
      <p>Account Balance: <span id="balance-display"></span> USD</p>
      <button onclick="cashOut()">Cash Out</button>
      <h2>Your Portfolio</h2>
      <table id="portfolio-table">
        <thead>
          <tr>
            <th>Team Symbol</th>
            <th>Team Name</th>
            <th>Quantity</th>
            <th>Current Price</th>
            <th>Total Value</th>
          </tr>
        </thead>
        <tbody id="portfolio-body"></tbody>
      </table>
    </div>
    
    <!-- Live Games Page -->
    <div id="liveGame" class="page">
      <h1>Live Games</h1>
      <div id="live-games-container"></div>
    </div>
    
    <!-- Stock Market Page -->
    <div id="stockMarket" class="page">
      <h1>Sports Stock Market</h1>
      <table id="stocks-table">
        <thead>
          <tr>
            <th>Team Symbol</th>
            <th>Team Name</th>
            <th>Price (USD)</th>
            <th>Change</th>
            <th>Action</th>
          </tr>
        </thead>
        <tbody id="stocks-body"></tbody>
      </table>
    </div>
    
    <!-- News Page -->
    <div id="news" class="page">
      <h1>Sports News Flash</h1>
      <div id="news-container"></div>
    </div>
    
    <!-- Instructions Page -->
    <div id="instructions" class="page">
      <h1>Instructions</h1>
      <p>Welcome to the Sports Stock Market Simulator! This is a fun, risk‑free game where you learn the basics of trading using fake money.</p>
      <ul>
        <li>You start with <strong>50,000 USD</strong>.</li>
        <li><strong>Dashboard:</strong> View your balance and portfolio (buy, sell, and track your sports team stocks).</li>
        <li><strong>Live Games:</strong> Bet on multiple simulated live games. If you win a bet, your wager doubles; if you lose, it’s lost. (Each game can be bet on only once per session.)</li>
        <li><strong>Stock Market:</strong> Buy and sell stocks representing USA sports teams (NFL, NBA, NHL, MLB, MLS). Prices fluctuate randomly.</li>
        <li><strong>News:</strong> Stay updated with fast‑paced, wild headlines.</li>
        <li><strong>Cash Out:</strong> When you’re ready, cash out from your Dashboard to celebrate your winnings (this resets the game).</li>
      </ul>
      <p>Good luck, make smart trades, and enjoy the neon‑fueled action!</p>
    </div>
    
    <!-- Cash Out / Celebration Page -->
    <div id="cashOut" class="page">
      <h1>Congratulations!</h1>
      <p>You cashed out with <span id="cashOut-amount"></span> USD!</p>
      <div id="confetti-container"></div>
      <button onclick="restartGame()">Restart Game</button>
    </div>
  </div>
  
  <!-- BOTTOM TICKER -->
  <div id="bottom-ticker">
    <p id="bottom-ticker-text"></p>
  </div>
  
  <script>
    document.addEventListener("DOMContentLoaded", function() {
      // Global Variables
      let balance = 0;
      let portfolio = {}; // { symbol: quantity }
      let stocks = [];    // Array of stock objects
      let liveGames = []; // Array of live game objects
      
      // TEAM ARRAYS
      const nflTeamNames = ["Arizona Cardinals", "Atlanta Falcons", "Baltimore Ravens", "Buffalo Bills", "Carolina Panthers", "Chicago Bears", "Cincinnati Bengals", "Cleveland Browns", "Dallas Cowboys", "Denver Broncos", "Detroit Lions", "Green Bay Packers", "Houston Texans", "Indianapolis Colts", "Jacksonville Jaguars", "Kansas City Chiefs", "Las Vegas Raiders", "Los Angeles Chargers", "Los Angeles Rams", "Miami Dolphins", "Minnesota Vikings", "New England Patriots", "New Orleans Saints", "New York Giants", "New York Jets", "Philadelphia Eagles", "Pittsburgh Steelers", "San Francisco 49ers", "Seattle Seahawks", "Tampa Bay Buccaneers", "Tennessee Titans", "Washington Commanders"];
      const nbaTeamNames = ["Atlanta Hawks", "Boston Celtics", "Brooklyn Nets", "Charlotte Hornets", "Chicago Bulls", "Cleveland Cavaliers", "Dallas Mavericks", "Denver Nuggets", "Detroit Pistons", "Golden State Warriors", "Houston Rockets", "Indiana Pacers", "Los Angeles Clippers", "Los Angeles Lakers", "Memphis Grizzlies", "Miami Heat", "Milwaukee Bucks", "Minnesota Timberwolves", "New Orleans Pelicans", "New York Knicks", "Oklahoma City Thunder", "Orlando Magic", "Philadelphia 76ers", "Phoenix Suns", "Portland Trail Blazers", "Sacramento Kings", "San Antonio Spurs", "Toronto Raptors", "Utah Jazz", "Washington Wizards"];
      const nhlTeamNames = ["Anaheim Ducks", "Arizona Coyotes", "Boston Bruins", "Buffalo Sabres", "Calgary Flames", "Carolina Hurricanes", "Chicago Blackhawks", "Colorado Avalanche", "Columbus Blue Jackets", "Dallas Stars", "Detroit Red Wings", "Edmonton Oilers", "Florida Panthers", "Los Angeles Kings", "Minnesota Wild", "Montreal Canadiens", "Nashville Predators", "New Jersey Devils", "New York Islanders", "New York Rangers", "Ottawa Senators", "Philadelphia Flyers", "Pittsburgh Penguins", "San Jose Sharks", "Seattle Kraken", "St. Louis Blues", "Tampa Bay Lightning", "Toronto Maple Leafs", "Vancouver Canucks", "Vegas Golden Knights", "Washington Capitals", "Winnipeg Jets"];
      const mlbTeamNames = ["Arizona Diamondbacks", "Atlanta Braves", "Baltimore Orioles", "Boston Red Sox", "Chicago Cubs", "Chicago White Sox", "Cincinnati Reds", "Cleveland Guardians", "Colorado Rockies", "Detroit Tigers", "Houston Astros", "Kansas City Royals", "Los Angeles Angels", "Los Angeles Dodgers", "Miami Marlins", "Milwaukee Brewers", "Minnesota Twins", "New York Yankees", "New York Mets", "Oakland Athletics", "Philadelphia Phillies", "Pittsburgh Pirates", "San Diego Padres", "San Francisco Giants", "Seattle Mariners", "St. Louis Cardinals", "Tampa Bay Rays", "Texas Rangers", "Toronto Blue Jays", "Washington Nationals"];
      const mlsTeamNames = ["Atlanta United FC", "Austin FC", "CF Montréal", "Charlotte FC", "Chicago Fire FC", "FC Cincinnati", "Columbus Crew", "D.C. United", "FC Dallas", "Houston Dynamo", "Inter Miami CF", "LA Galaxy", "Los Angeles FC", "Minnesota United FC", "Nashville SC", "New England Revolution", "New York City FC", "New York Red Bulls", "Orlando City SC", "Philadelphia Union", "Portland Timbers", "Real Salt Lake", "San Jose Earthquakes", "Seattle Sounders FC", "Sporting Kansas City", "Vancouver Whitecaps FC"];
      
      // USER DATA FUNCTIONS
      function loadUserData() {
        balance = parseFloat(localStorage.getItem("balance"));
        if (isNaN(balance)) { balance = 50000; }
        const port = localStorage.getItem("portfolio");
        portfolio = port ? JSON.parse(port) : {};
      }
      function saveUserData() {
        localStorage.setItem("balance", balance);
        localStorage.setItem("portfolio", JSON.stringify(portfolio));
      }
      loadUserData();
      
      // GLOBAL TICKERS
      function updateGlobalTicker() {
        const tickerHTML = `<span style="color: red; font-family: Arial;">Balance: ${balance.toFixed(2)} USD</span> ` +
                           `<span style="color: orange; font-family: Courier New;">| Stocks Live |</span> ` +
                           `<span style="color: lime; font-family: Impact;">| Live Games |</span> ` +
                           `<span style="color: blue; font-family: Georgia;">| Crazy News |</span>`;
        document.getElementById("ticker-text").innerHTML = tickerHTML;
      }
      updateGlobalTicker();
      setInterval(updateGlobalTicker, 5000);
      function updateBottomTicker() {
        let tickerStr = "";
        for (let i = 0; i < Math.min(20, stocks.length); i++) {
          tickerStr += `${stocks[i].symbol}: $${stocks[i].price.toFixed(2)} | `;
        }
        document.getElementById("bottom-ticker-text").innerText = tickerStr;
      }
      updateBottomTicker();
      setInterval(updateBottomTicker, 5000);
      
      // DASHBOARD UPDATE
      function updateDashboard() {
        document.getElementById("balance-display").innerText = balance.toFixed(2);
        const tbody = document.getElementById("portfolio-body");
        tbody.innerHTML = "";
        for (const sym in portfolio) {
          const qty = portfolio[sym];
          const stock = stocks.find(s => s.symbol === sym) || { name: "N/A", price: 0 };
          const totalValue = qty * stock.price;
          const row = document.createElement("tr");
          row.innerHTML = `<td>${sym}</td>
                           <td>${stock.name}</td>
                           <td>${qty}</td>
                           <td>${stock.price.toFixed(2)}</td>
                           <td>${totalValue.toFixed(2)}</td>`;
          tbody.appendChild(row);
        }
      }
      
      // PAGE NAVIGATION
      function showSection(sectionId) {
        const pages = document.getElementsByClassName("page");
        for (let i = 0; i < pages.length; i++) {
          pages[i].classList.remove("active");
        }
        document.getElementById(sectionId).classList.add("active");
        if (sectionId === "dashboard") { updateDashboard(); }
        if (sectionId === "stockMarket") { updateStocksTable(); }
        if (sectionId === "liveGame") { 
          generateLiveGames();
          updateLiveGamesDisplay();
        }
      }
      window.showSection = showSection;
      
      // STOCK MARKET FUNCTIONS
      function generateSymbol(teamName) {
        const words = teamName.split(" ");
        let symbol = words.map(word => word.charAt(0)).join("").toUpperCase();
        if (symbol.length < 3) {
          symbol += teamName.replace(/\s+/g, "").substring(0, 3 - symbol.length).toUpperCase();
        }
        return symbol;
      }
      function generateStocks() {
        stocks = [];
        const addTeams = (teamArray, league) => {
          teamArray.forEach(team => {
            const symbol = generateSymbol(team);
            const price = parseFloat((Math.random() * 490 + 10).toFixed(2));
            const volatility = parseFloat((Math.random() * 0.18 + 0.02).toFixed(3));
            stocks.push({
              symbol,
              name: team,
              league,
              description: `${team} are a proud member of the ${league}.`,
              price,
              volatility,
              lastPrice: price
            });
          });
        };
        addTeams(nflTeamNames, "NFL");
        addTeams(nbaTeamNames, "NBA");
        addTeams(nhlTeamNames, "NHL");
        addTeams(mlbTeamNames, "MLB");
        addTeams(mlsTeamNames, "MLS");
      }
      generateStocks();
      function updateStocksTable() {
        const tbody = document.getElementById("stocks-body");
        tbody.innerHTML = "";
        stocks.forEach(stock => {
          const changeStr = stock.change >= 0 ? "+" + stock.change.toFixed(2) : stock.change.toFixed(2);
          const row = document.createElement("tr");
          row.innerHTML = `<td>${stock.symbol}</td>
                           <td title="${stock.description}">${stock.name}</td>
                           <td>${stock.price.toFixed(2)}</td>
                           <td style="color: ${stock.change >= 0 ? 'lime' : 'red'};">${changeStr}</td>
                           <td>
                             <button onclick="buyStock('${stock.symbol}')">Buy</button>
                             <button onclick="sellStock('${stock.symbol}')">Sell</button>
                           </td>`;
          tbody.appendChild(row);
        });
      }
      function updateStockPrices() {
        stocks.forEach(stock => {
          stock.lastPrice = stock.price;
          let changeFactor = (Math.random() - 0.5) * stock.volatility;
          if (Math.random() < 0.05) { changeFactor *= 5; }
          stock.price = Math.max(0.01, stock.price * (1 + changeFactor));
          stock.price = parseFloat(stock.price.toFixed(2));
          stock.change = stock.price - stock.lastPrice;
        });
        updateStocksTable();
        updateBottomTicker();
        updateGlobalTicker();
      }
      setInterval(updateStockPrices, 3000);
      function buyStock(symbol) {
        let stock = stocks.find(s => s.symbol === symbol);
        let qty = parseInt(prompt("Enter quantity to buy:", "100"));
        if (isNaN(qty) || qty <= 0) return;
        let cost = stock.price * qty;
        if (cost > balance) {
          alert("Insufficient funds!");
          return;
        }
        balance -= cost;
        portfolio[symbol] = (portfolio[symbol] || 0) + qty;
        saveUserData();
        updateDashboard();
        updateGlobalTicker();
      }
      window.buyStock = buyStock;
      function sellStock(symbol) {
        let stock = stocks.find(s => s.symbol === symbol);
        let owned = portfolio[symbol] || 0;
        let qty = parseInt(prompt("Enter quantity to sell:", "100"));
        if (isNaN(qty) || qty <= 0) return;
        if (qty > owned) {
          alert("You don't own that many shares!");
          return;
        }
        let revenue = stock.price * qty;
        balance += revenue;
        portfolio[symbol] = owned - qty;
        if (portfolio[symbol] === 0) { delete portfolio[symbol]; }
        saveUserData();
        updateDashboard();
        updateGlobalTicker();
      }
      window.sellStock = sellStock;
      /***** LIVE GAMES FUNCTIONS *****/
      function generateLiveGames() {
        liveGames = [];
        for (let i = 0; i < 3; i++) {
          let teamA = nflTeamNames[Math.floor(Math.random() * nflTeamNames.length)];
          let teamB;
          do { teamB = nflTeamNames[Math.floor(Math.random() * nflTeamNames.length)]; }
          while (teamB === teamA);
          let scoreA = Math.floor(Math.random() * 50);
          let scoreB = Math.floor(Math.random() * 50);
          liveGames.push({
            teamA,
            teamB,
            scoreA,
            scoreB,
            betPlaced: false,
            betAmount: 0,
            result: ""
          });
        }
      }
      function updateLiveGamesDisplay() {
        const container = document.getElementById("live-games-container");
        container.innerHTML = "";
        liveGames.forEach((game, index) => {
          const gameDiv = document.createElement("div");
          gameDiv.className = "live-game-event";
          gameDiv.innerHTML = `<strong>${game.teamA} ${game.scoreA} - ${game.scoreB} ${game.teamB}</strong><br>`;
          if (!game.betPlaced) {
            gameDiv.innerHTML += `Bet Amount: <input type="number" id="bet-${index}" placeholder="USD" min="1" style="width:70px;"> `;
            gameDiv.innerHTML += `<button onclick="betOnLiveGame(${index})">Place Bet</button>`;
          } else {
            gameDiv.innerHTML += `<em>${game.result}</em>`;
          }
          container.appendChild(gameDiv);
        });
      }
      function betOnLiveGame(index) {
        const input = document.getElementById("bet-" + index);
        const amount = parseFloat(input.value);
        if (!amount || amount <= 0) {
          alert("Enter a valid bet amount.");
          return;
        }
        if (amount > balance) {
          alert("Insufficient funds!");
          return;
        }
        balance -= amount;
        const win = Math.random() < 0.5;
        if (win) {
          balance += amount * 2;
          liveGames[index].result = "You won! Your bet doubled.";
        } else {
          liveGames[index].result = "You lost your bet.";
        }
        liveGames[index].betPlaced = true;
        saveUserData();
        updateDashboard();
        updateGlobalTicker();
        updateLiveGamesDisplay();
      }
      window.betOnLiveGame = betOnLiveGame;
      /***** NEWS FUNCTIONS *****/
      const newsHeadlines = [
        "LeBron James announces surprise retirement—then un-retires 10 minutes later!",
        "Patriots sign unknown kicker who can hit 80-yard field goals!",
        "Jason Tatum plays full game in ski boots—still drops 40 points!",
        "Yankees win 30-0, but the scoreboard malfunctions and reads 3-0!",
        "Giannis grows two inches overnight—NBA investigates!",
        "Cowboys forget to bring jerseys, play game in T-shirts from the gift shop!",
        "Celtics' mascot accidentally ejected from game after altercation with referee!",
        "Warriors attempt full-game half-court shots—still win by 15!",
        "Dolphins sign world’s fastest sprinter—his route-running is awful!",
        "Broncos' coach calls time-out every play in first quarter—NFL confused!",
        "Lakers’ stadium ceiling collapses—game continues outside in parking lot!",
        "NHL team replaces goalie with brick wall—league unsure how to handle it!",
        "Cardinals win game despite having negative total yardage!",
        "76ers announce they are moving to Mars for “better altitude training!”",
        "Bulls' new rookie plays in rollerblades—scores 50!",
        "Red Sox hire retired pitcher just for ceremonial first pitch—he throws 9 perfect innings!",
        "New York Jets rename themselves the New York Helicopters!",
        "Packers play entire game without a quarterback—still win!",
        "NFL bans touchdown celebrations—players invent secret hand signals instead!",
        "Mavericks coach challenges every single referee call—game lasts 7 hours!",
        "PGA Tour allows golf carts—Tiger Woods wins tournament without walking!",
        "Raiders’ QB throws ball so hard it gets lodged in the goalpost!",
        "Bears' linebacker tackles wrong player—on his own team!",
        "Dodgers sign a baseball robot—MLB says it’s fine!",
        "Heat fans demand refund after team scores only 9 points in first half!",
        "Suns announce they will only shoot three-pointers this season!",
        "New rule: NBA players can challenge referee fouls via rock-paper-scissors!",
        "Giants win game 2-0 after both teams forget how to score!",
        "MLS team signs a kangaroo as their new goalie!",
        "Ravens attempt onside kick on every kickoff—NFL forced to step in!",
        "Nets win game without making a single two-point shot!",
        "Colts kicker breaks record with 75-yard field goal—ball still hasn’t landed!",
        "Steelers attempt trick play where entire team hides in the endzone!",
        "Bucks’ mascot challenges entire team to 1v5—scores 8 points!",
        "Astros use laser pointers to blind opposing batters—MLB investigation pending!",
        "Rams’ mascot gets ejected for taunting opposing coach!",
        "Seahawks introduce new strategy: No punting, ever!",
        "Clippers wear sunglasses during night game—turns out, bad idea!",
        "Cubs field a team of only pitchers—somehow, they win!",
        "WNBA team signs retired NFL player as a publicity stunt—he gets dunked on!",
        "Lions’ quarterback throws the football into the stands—turns out, it was fourth down!",
        "Mariners attempt to steal every base in one inning—only one player succeeds!",
        "NBA allows team to play with 8 players at once due to “clerical error!”",
        "Browns sign new kicker after he makes a 90-yard field goal in pregame warmups!",
        "Umpire calls strike before pitch is even thrown—somehow, he's right!",
        "Eagles coach forgets to call plays—team just starts improvising!",
        "Hornets introduce new uniform made entirely of LED lights!",
        "Rockets mascot replaces injured player in 4th quarter—hits game-winner!",
        "Jets' running back accidentally runs into locker room mid-play!",
        "Soccer team wins 1-0 without taking a single shot on goal—what happened?!",
        "Player gets ejected for wearing the wrong color shoelaces!",
        "Team attempts to play game with only five total players—immediate disaster!",
        "Basketball player tries dunking from half-court—somehow lands in the stands!",
        "Hockey player forgets skates—plays game in sneakers!",
        "Tennis player refuses to use racket—wins match with just his hand!",
        "Football team replaces offensive linemen with sumo wrestlers!",
        "Racing driver forgets pit stop—finishes race with three wheels!",
        "Fighter accidentally punches referee—immediately loses via DQ!",
        "Olympic sprinter outruns security after forgetting credential!",
        "Golf tournament ends in chaos as all players hit the same ball!",
        "Cyclist attempts to bunny-hop over finish line—crashes spectacularly!",
        "Soccer goalie catches fireball during free kick—league investigates!",
        "Wrestler wins championship belt—refuses to give it back!",
        "NBA player attempts alley-oop to himself off referee’s head!",
        "Baseball team fields nine identical twins—opposing team totally confused!",
        "MMA fighter brings folding chair into the octagon—declared instant winner!",
        "Boxer accidentally knocks himself out—his opponent celebrates in confusion!",
        "NFL team replaces punter with quarterback—passes every fourth down!",
        "Basketball player demands free throws after tripping over shoelace!",
        "Player scores own goal in overtime—celebrates anyway!",
        "Track and field event halted due to herd of escaped cows!",
        "Baseball team forgets to bring gloves—uses bare hands!",
        "Wrestling match interrupted by unexpected ladder—nobody knows why!",
        "Team tries to play entire season using only their backups—0-82!",
        "Soccer team tries to freeze time by standing still for 90 minutes!"
      ];
      function updateNews() {
        const container = document.getElementById("news-container");
        const item = document.createElement("div");
        item.className = "news-item";
        const headline = newsHeadlines[Math.floor(Math.random() * newsHeadlines.length)];
        item.innerText = headline;
        container.prepend(item);
        if (container.childNodes.length > 20) {
          container.removeChild(container.lastChild);
        }
      }
      setInterval(updateNews, 4000);
      
      /***** CASH OUT & CELEBRATION *****/
      function cashOut() {
        const pages = document.getElementsByClassName("page");
        for (let i = 0; i < pages.length; i++) {
          pages[i].classList.remove("active");
        }
        document.getElementById("cashOut").classList.add("active");
        document.getElementById("cashOut-amount").innerText = balance.toFixed(2);
        launchConfetti();
      }
      window.cashOut = cashOut;
      
      function restartGame() {
        localStorage.clear();
        location.reload();
      }
      window.restartGame = restartGame;
      
      function launchConfetti() {
        const container = document.getElementById("confetti-container");
        container.innerHTML = "";
        for (let i = 0; i < 100; i++) {
          const confetti = document.createElement("div");
          confetti.className = "confetti";
          confetti.style.left = Math.random() * 100 + "%";
          confetti.style.backgroundColor = "hsl(" + Math.random() * 360 + ", 100%, 50%)";
          container.appendChild(confetti);
          setTimeout(() => confetti.remove(), 3000);
        }
      }
      const confettiStyle = document.createElement("style");
      confettiStyle.innerHTML = `
        #confetti-container {
          position: fixed;
          top: 0;
          left: 0;
          width: 100%;
          height: 100%;
          pointer-events: none;
          z-index: 200;
        }
        .confetti {
          position: absolute;
          top: -10px;
          width: 10px;
          height: 10px;
          opacity: 0.8;
          animation: confettiFall 3s linear forwards;
        }
        @keyframes confettiFall {
          0% { transform: translateY(0) rotate(0deg); }
          100% { transform: translateY(100vh) rotate(360deg); }
        }
      `;
      document.head.appendChild(confettiStyle);
      
      /***** INITIALIZATION *****/
      updateStocksTable();
      updateDashboard();
      generateLiveGames();
      updateLiveGamesDisplay();
      setInterval(updateStockPrices, 3000);
      
      /***** EXPOSE FUNCTIONS TO GLOBAL SCOPE *****/
      window.buyStock = buyStock;
      window.sellStock = sellStock;
      window.betOnLiveGame = betOnLiveGame;
    });
  </script>
</body>
</html>
