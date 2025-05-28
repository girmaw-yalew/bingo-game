<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="description" content="Interactive Bingo Game (200 Cards) with Stats, Betting, Locking, Board-Click Card Registration - Simplified">
  <title>Maraki Bingo</title>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" integrity="sha512-9usAa10IRO0HhonpyAIVpjrylPvoDwiPUiKdWk5t3PyolY1cOd4DSE0Ga+ri4AuTroPR5aQvXU9xC6qOPnzFeg==" crossorigin="anonymous" referrerpolicy="no-referrer" />


  
 

   
                 <i class="fas fa-info-circle"></i> <span class="button-text-small">Rules</span>
             </button>
         </div>

        <!-- Called Number Area -->
        <div class="below-board-displays-container">
            <div id="special-called-number-display-wrapper">
                <div id="called-number">--</div>
                <div id="immediately-preceding-called-number" class="last-number-circle" style="display: none;"></div> <!-- New element -->
            </div>
            <div class="info-displays">
                <div class="info-column left">
                    <div id="last-five-wrapper" class="last-numbers-wrapper left"></div>
                </div>
                <div class="info-column right">
                    <div id="called-number-right">--</div>
                    <div id="last-two-wrapper" class="last-numbers-wrapper right"></div>
                </div>
            </div>
        </div>

         <!-- Main Game Actions Panel -->
         <div id="main-actions-panel">
            <div>
                <button class="button" id="start-button">Start Game</button>
                <button class="button" id="pause-button">Stop Game</button>
            </div>
            <div>
                <button class="button danger" id="reset-button">Clear Game</button>
            </div>
            <div id="winner-search-container-wrapper">
                <div id="winner-search-container-moved" style="display: flex; align-items: center; gap: 10px;">
                    <input type="number" id="winner-search-input" class="search-input betting-input" placeholder="Enter Card No. (1-200)" min="1" max="200" style="max-width: 160px;">
                    <button class="button blue" id="winner-search-button" title="Check specific card against win condition">Check Card</button>
                </div>
            </div>
            <div>
                <button class="button purple" id="shuffle-button">Shuffle Numbers</button>
                <button class="button purple" id="stop-shuffle-button" style="display: none;">Stop Shuffling</button>
            </div>
            <div style="flex-direction: column; align-items: center;">
                <label for="stake-per-player" class="betting-label">Stake per Player (ETB):</label>
                <input type="number" id="stake-per-player" class="search-input betting-input" min="10" step="10" value="10" style="max-width: 100px; margin-bottom: 3px;">
                <button id="set-stake-button" class="button blue betting-button">Set</button>
            </div>
            <!------------------- Set Balance Controls --------------------------------------------------------------------------------->
             <div style="flex-direction: column; align-items: center; margin-top: 5px;">
                 <label for="set-balance-input" class="betting-label"></label>
                 <input type="number" id="set-balance-input" class="search-input betting-input" min="0" step="1" placeholder="Enter new balance" style="max-width: 130px; margin-bottom: 3px;">
                 <button id="set-balance-button" class="button blue betting-button">Set Balance</button>
            </div>
            
            <!-- Hidden Toggle Cards Button Container -->
            <div>
                <button class="button" id="toggle-cards-button">Hide Cards</button>
            </div>
         </div>

        <!-- Win Threshold Selector -->
        <div class="win-threshold-selector">
            <label for="required-patterns-select">Require</label>
            <select id="required-patterns-select">
                <option value="1">1</option> <option value="2" selected>2</option> <option value="3">3</option> <option value="4">4</option> <option value="5">5</option> <option value="6">6</option> <option value="7">7</option> <option value="8">8</option> <option value="9">9</option> <option value="10">10</option> <option value="11">11</option> <option value="12">12</option> <option value="13">13</option>
            </select>
            <label for="required-patterns-select">Pattern(s) to Win</label>
        </div>

         <!-- Bet/Derash Display Circle -->
         <div id="board-bet-info" class="board-bet-info-display">
             <div>Total Bet: <span id="board-total-stake-display">0</span> ETB</div>
             <div><span id="board-derash-display">0</span></div>
         </div>

         <!-- Small Speed, Volume -->
         <div id="mini-info-bar">
            <div class="speed-controls">
                <button class="button speed-adjust" id="speed-decrease-button" title="Decrease call speed (calls slower)">-</button>
                <span id="current-speed-display">Speed: 2.0s</span>
                <button class="button speed-adjust" id="speed-increase-button" title="Increase call speed (calls faster)">+</button>
            </div>
            <span id="call-count-display">Calls: 0</span>
            <div class="volume-container">
                <label for="volume-control" class="volume-label">Volume:</label>
                <input type="range" id="volume-control" class="volume-control" min="0" max="1" step="0.1" value="0.5">
            </div>
         </div>

         <div class="central-quick-controls"></div>

         <div class="registration-nav-controls" id="reg-nav-controls">
             <button class="reg-nav-button" id="reg-nav-1-100" data-range="1-100">Cards 1-100</button>
             <button class="reg-nav-button" id="reg-nav-101-200" data-range="101-200">Cards 101-200</button>
         </div>

    </div>

    <div id="shuffle-display" class="shuffle-display" style="display: none;">B-12</div>

    <div class="game-stats-container">
      <div class="stat-row">
          <div class="stat-item stat-total-games">
              <span class="stat-label">Total Games Played</span>
              <span id="total-games-played-display" class="stat-value stat-rect">0</span>
          </div>
          <div class="stat-item stat-bet-amount">
               <span class="stat-label">Current Derash (ETB)</span>
              <div id="bet-amount-display" class="stat-value stat-circle">0</div>
          </div>
      </div>
      <div class="stat-row stat-row-icons">
           <div class="stat-item stat-icon">
               <i class="fas fa-calendar-day"></i>
               <span id="daily-games-played-display" class="stat-value">0</span>
               <span class="stat-label-icon">Daily Games</span>
           </div>
           <div class="stat-item stat-icon">
               <i class="fas fa-coins"></i>
               <span id="daily-earnings-display" class="stat-value">0</span>
                <span class="stat-label-icon">Daily Earn</span>
           </div>
            <div class="stat-item stat-icon">
               <i class="fas fa-chart-line"></i>
               <span id="total-earnings-display" class="stat-value">0</span>
                <span class="stat-label-icon">Total Earn</span>
           </div>
           <div class="stat-item stat-icon">
               <i class="fas fa-wallet"></i>
               <span id="wallet-balance-display" class="stat-value">1000</span>
               <span class="stat-label-icon">Balance</span>
           </div>
      </div>
    </div>

    <div class="bingo-cards-container" id="bingo-cards-container"></div>

  </div>

  <script>    // Constants and State Variables
  // Constants and State Variables
    const BINGO_HEADERS = ['B', 'I', 'N', 'G', 'O'];
    const COLUMN_RANGES = { B: [1, 15], I: [16, 30], N: [31, 45], G: [46, 60], O: [61, 75] };
    const TOTAL_CARDS = 200;
    const CARD_LAYOUT_STORAGE_KEY = 'bingoCardLayouts_v12_simple';
    const SETTINGS_STORAGE_KEY = 'bingoGameSettings_v12_simple';
    const BASIC_WIN_CALL_COUNT = 15;
    const REGISTRATION_PAGE_SIZE = 100;
    const FEE_PERCENTAGE = 20;

    const calledNumbers = new Set();
    const calledNumberHistory = [];
    const cardLayouts = new Map();
    const cardElements = new Map();
    const fixedCardLayouts = new Map();
    const winners = new Set();
    const cardStates = new Map();

    let intervalId = null;
    let isGameRunning = false;
    let callSpeed = 2000;
    const SPEED_INCREMENT = 250; const MIN_SPEED = 500; const MAX_SPEED = 5000;
    let isShuffling = false;
    let shuffleIntervalId = null;
    let currentShuffleNumbers = [];
    let shuffleDisplayTimeout = null;
    let requiredPatternCount = 2;
    let callCount = 0;
    let lastCalledInfo = null;
    let activeRegistrationRange = null;
    const registeredNumbers = new Set();

    let isInPreGameMode = false;
    let preGameActiveRange = '1-100';

    let totalGamesPlayed = 0;
    let dailyGamesPlayed = 0;
    let dailyEarnings = 0;
    let totalEarnings = 0;
    let walletBalance = 1000;
    let currentStakePerPlayer = 10;
    let currentTotalStake = 0;
    let currentFee = 0;
    let currentDerash = 0;

    // DOM Selectors
    const bodyElement = document.body;
    const calledNumberDisplay = document.getElementById('called-number');
    const lastFiveWrapper = document.getElementById('last-five-wrapper');
    const lastTwoWrapper = document.getElementById('last-two-wrapper');
    const volumeControl = document.getElementById('volume-control');
    const themeToggle = document.getElementById('theme-toggle');
    const speedDecreaseButton = document.getElementById('speed-decrease-button');
    const speedIncreaseButton = document.getElementById('speed-increase-button');
    const currentSpeedDisplay = document.getElementById('current-speed-display');
    const callCountDisplay = document.getElementById('call-count-display');
    const callCountCircleDisplay = document.getElementById('call-count-circle-display');
    const startButton = document.getElementById('start-button');
    const pauseButton = document.getElementById('pause-button');
    const resetButton = document.getElementById('reset-button');
    const shuffleButton = document.getElementById('shuffle-button');
    const stopShuffleButton = document.getElementById('stop-shuffle-button');
    const shuffleDisplayElement = document.getElementById('shuffle-display');
    const boardElement = document.getElementById('bingo-board');
    const cardsContainer = document.getElementById('bingo-cards-container');
    const winnerSearchInput = document.getElementById('winner-search-input');
    const winnerSearchButton = document.getElementById('winner-search-button');
    const requiredPatternsSelect = document.getElementById('required-patterns-select');
    const audioElements = {
        callSound: document.getElementById('call-sound'),
        winnerSound: document.getElementById('winner-sound'),
        shuffleSound: document.getElementById('shuffle-sound'),
        shuffleStopSound: document.getElementById('shuffle-stop-sound'),
        startSound: document.getElementById('start-sound'),
        pauseSound: document.getElementById('pause-sound'),
        resetSound: document.getElementById('reset-sound'),
        errorSound: document.getElementById('error-sound'),
        lockedSound: document.getElementById('locked-sound'),
        frozenSound: document.getElementById('frozen-sound'),
        basicWinSound: document.getElementById('basic-win-sound'),
        blockCardSound: document.getElementById('block-card-sound')
    };
    const customAlertOverlay = document.getElementById('custom-alert-overlay');
    const customAlertBox = document.getElementById('custom-alert-box');
    const customAlertMessage = document.getElementById('custom-alert-message');
    const customAlertOkButton = document.getElementById('custom-alert-ok-button');
    const regNavControls = document.getElementById('reg-nav-controls');
    const regNavButton1_100 = document.getElementById('reg-nav-1-100');
    const regNavButton101_200 = document.getElementById('reg-nav-101-200');
    const totalGamesPlayedDisplay = document.getElementById('total-games-played-display');
    const betAmountDisplay = document.getElementById('bet-amount-display');
    const dailyGamesPlayedDisplay = document.getElementById('daily-games-played-display');
    const dailyEarningsDisplay = document.getElementById('daily-earnings-display');
    const totalEarningsDisplay = document.getElementById('total-earnings-display');
    const walletBalanceDisplay = document.getElementById('wallet-balance-display');
    const stakePerPlayerInput = document.getElementById('stake-per-player');
    const setStakeButton = document.getElementById('set-stake-button');
    const boardDerashDisplay = document.getElementById('board-derash-display');
    const actionManualCall = document.getElementById('action-manual-call');
    const actionReannounce = document.getElementById('action-reannounce');
    const actionFindNumBoard = document.getElementById('action-find-num-board');
    const actionQuickRules = document.getElementById('action-quick-rules');
    const playerCountDisplayElement = document.getElementById('player-count-display');
    const preGameControlsContainer = document.getElementById('pre-game-controls-container');
    const preGameStartButton = document.getElementById('pre-game-start-button');
    const preGameClearRegistrationsButton = document.getElementById('pre-game-clear-registrations-button');
    const preGameRegNav1_100 = document.getElementById('pre-game-reg-nav-1-100');
    const preGameRegNav101_200 = document.getElementById('pre-game-reg-nav-101-200');
    const backToGameBoardButton = document.getElementById('back-to-game-board-button');
    const setBalanceInput = document.getElementById('set-balance-input'); // Added
    const setBalanceButton = document.getElementById('set-balance-button'); // Added

    // --- Helper Functions ---
    function handleUnzoom(cardElement) {
        if (!cardElement || !cardElement.classList.contains('zoomed-card')) return;
        cardElement.classList.remove('zoomed-card', 'awaiting-exclusion-decision');
        setMessageOnCard(cardElement, null, null);
        clearBasicWinBoardHighlights();
    }

    function seededRandom(seed) { const x = Math.sin(seed) * 10000; return x - Math.floor(x); }
    function generateDeterministicNumbers(count, min, max, cardId, columnIndex) { const nums = new Set(); let attempts = 0; const maxAttempts = 100; const seed = cardId * 100 + columnIndex; while (nums.size < count && attempts < maxAttempts) { const randomValue = seededRandom(seed + attempts * 0.1); const num = Math.floor(randomValue * (max - min + 1)) + min; nums.add(num); attempts++; } return Array.from(nums); }
    function createConfetti() { const clrs = ['#f44336', '#e91e63', '#9c27b0', '#673ab7', '#3f51b5', '#2196f3', '#03a9f4', '#00bcd4', '#009688', '#4caf50', '#8bc34a', '#cddc39', '#ffeb3b', '#ffc107', '#ff9800', '#ff5722']; for (let i = 0; i < 100; i++) { const c = document.createElement('div'); c.className = 'confetti'; c.style.left = `${Math.random()*100}vw`; c.style.backgroundColor = clrs[Math.floor(Math.random()*clrs.length)]; c.style.width = `${Math.random()*10+5}px`; c.style.height = c.style.width; c.style.animationDuration = `${Math.random()*3+2}s`; document.body.appendChild(c); setTimeout(() => c.remove(), 5000); } }
    function changeBoardColor(color) { if (activeRegistrationRange || isInPreGameMode) return; boardElement.className = 'bingo-board'; if (color) { boardElement.classList.add(`custom-${color}`); } updateBoardHighlights(); console.log(`Board color set to: ${color || 'default'}`); }
    function playNumberSound(header, number) { if (!header || !number) { return; } const filename = `${header}-${number}.mp3`; const audioPath = `audio/${filename}`; const numberAudio = new Audio(audioPath); numberAudio.volume = volumeControl.value; numberAudio.play().catch(error => { console.warn(`Audio ${audioPath} not found or error:`, error); if (audioElements.callSound) audioElements.callSound.play().catch(e => console.error("Fallback sound error:", e)); }); }
    function playSound(audioElement) { if (audioElement) { audioElement.currentTime = 0; audioElement.volume = volumeControl.value; audioElement.play().catch(e => console.error(`Sound ${audioElement.id} error:`, e)); } else { console.warn("Attempted to play null sound"); } }
    function loadCardLayouts() { try { const savedLayouts = localStorage.getItem(CARD_LAYOUT_STORAGE_KEY); if (savedLayouts) { const parsedLayouts = JSON.parse(savedLayouts); Object.entries(parsedLayouts).forEach(([cardId, layout]) => { fixedCardLayouts.set(parseInt(cardId, 10), layout); }); return true; } } catch (error) { console.error("Layout load error:", error); localStorage.removeItem(CARD_LAYOUT_STORAGE_KEY); } return false; }
    function saveCardLayouts() { try { const layoutsObj = {}; fixedCardLayouts.forEach((layout, cardId) => { layoutsObj[cardId] = layout; }); localStorage.setItem(CARD_LAYOUT_STORAGE_KEY, JSON.stringify(layoutsObj)); } catch (error) { console.error("Layout save error:", error); } }

    function loadSettings() {
        try {
            const savedSettings = localStorage.getItem(SETTINGS_STORAGE_KEY);
            if (savedSettings) {
                const settings = JSON.parse(savedSettings);
                requiredPatternCount = parseInt(settings.requiredPatternCount || '2', 10);
                if (isNaN(requiredPatternCount) || requiredPatternCount < 1 || requiredPatternCount > 13) requiredPatternCount = 2;
                requiredPatternsSelect.value = requiredPatternCount.toString();
                callSpeed = parseInt(settings.callSpeed || '2000', 10);
                if (settings.theme === 'light') { document.body.classList.add('light-theme'); themeToggle.textContent = '🌙'; }
                else { document.body.classList.remove('light-theme'); themeToggle.textContent = '☀️'; }
                totalGamesPlayed = parseFloat(settings.totalGamesPlayed || '0');
                dailyGamesPlayed = parseInt(settings.dailyGamesPlayed || '0', 10);
                dailyEarnings = parseFloat(settings.dailyEarnings || '0');
                totalEarnings = parseFloat(settings.totalEarnings || '0');
                walletBalance = parseFloat(settings.walletBalance || '1000'); // Keep default low or adjust as needed
                currentStakePerPlayer = parseInt(settings.currentStakePerPlayer || '10', 10);
                registeredNumbers.clear();
                if (settings.registeredNumbers && Array.isArray(settings.registeredNumbers)) { settings.registeredNumbers.forEach(num => { if(typeof num === 'number' && num >= 1 && num <= TOTAL_CARDS) registeredNumbers.add(num); }); }
                if (settings.cardStates) { Object.entries(settings.cardStates).forEach(([cardIdStr, state]) => { const cardId = parseInt(cardIdStr, 10); if (!isNaN(cardId)) { if (registeredNumbers.has(cardId)) { cardStates.set(cardId, state); if (state === 'winner' || state === 'basic') { winners.add(cardId); } } else if (state === 'user-excluded') { cardStates.set(cardId, state); } } }); }
            } else { requiredPatternsSelect.value = requiredPatternCount.toString(); }
            stakePerPlayerInput.value = currentStakePerPlayer;
        } catch (error) { console.error(`Settings load error (${SETTINGS_STORAGE_KEY}):`, error); localStorage.removeItem(SETTINGS_STORAGE_KEY); requiredPatternsSelect.value = requiredPatternCount.toString(); stakePerPlayerInput.value = currentStakePerPlayer; }
        updatePlayerCountDisplay(); updateStatsDisplay();
    }
    function saveSettings() {
        try {
            const serializableCardStates = {}; cardStates.forEach((state, cardId) => { serializableCardStates[cardId] = state; });
            const settings = { requiredPatternCount: requiredPatternCount, callSpeed: callSpeed, theme: document.body.classList.contains('light-theme') ? 'light' : 'dark', registeredNumbers: Array.from(registeredNumbers), totalGamesPlayed: totalGamesPlayed, dailyGamesPlayed: dailyGamesPlayed, dailyEarnings: dailyEarnings, totalEarnings: totalEarnings, walletBalance: walletBalance, currentStakePerPlayer: currentStakePerPlayer, cardStates: serializableCardStates };
            localStorage.setItem(SETTINGS_STORAGE_KEY, JSON.stringify(settings));
        } catch (error) { console.error(`Settings save error (${SETTINGS_STORAGE_KEY}):`, error); }
    }

    function updatePlayerCountDisplay() { if (playerCountDisplayElement) { playerCountDisplayElement.textContent = registeredNumbers.size; } }
    function updateSpeedDisplay() { if (currentSpeedDisplay) { currentSpeedDisplay.textContent = `Speed: ${(callSpeed / 1000).toFixed(1)}s`; } }
    function updateCallCountDisplay() { if (callCountDisplay) { callCountDisplay.textContent = `Calls: ${callCount}`; } if (callCountCircleDisplay) { callCountCircleDisplay.textContent = callCount; } }
    function updateStatsDisplay() { if (totalGamesPlayedDisplay) totalGamesPlayedDisplay.textContent = totalGamesPlayed.toLocaleString(undefined, {minimumFractionDigits: 0, maximumFractionDigits: 1}); if (betAmountDisplay) betAmountDisplay.textContent = `${currentDerash.toFixed(0)}`; if (dailyGamesPlayedDisplay) dailyGamesPlayedDisplay.textContent = dailyGamesPlayed; if (dailyEarningsDisplay) dailyEarningsDisplay.textContent = `${dailyEarnings.toFixed(0)}`; if (totalEarningsDisplay) totalEarningsDisplay.textContent = `${totalEarnings.toFixed(0)}`; if (walletBalanceDisplay) walletBalanceDisplay.textContent = `${walletBalance.toLocaleString()}`; if (boardDerashDisplay) { boardDerashDisplay.textContent = currentDerash.toFixed(0); } } // Used toLocaleString for balance
    function calculateBetting(stake) { currentStakePerPlayer = stake; const players = registeredNumbers.size > 0 ? registeredNumbers.size : 0; if (players === 0) { currentTotalStake = 0; currentFee = 0; currentDerash = 0; } else { currentTotalStake = players * currentStakePerPlayer; if (players <= 5) { currentFee = 0; currentDerash = currentTotalStake; } else { currentFee = currentTotalStake * (FEE_PERCENTAGE / 100); currentDerash = currentTotalStake - currentFee; } } updateStatsDisplay(); saveSettings(); return { fee: currentFee, derash: currentDerash, totalStake: currentTotalStake }; }

    function setBoardLayout(type) {
        boardElement.innerHTML = ''; boardElement.numberCellsMap = null; boardElement.classList.remove('registration-view', 'pre-game-active-board-style');
        if (type === 'standard') {
            bodyElement.classList.remove('pre-game-active', 'registration-active');
            const screenWidth = window.innerWidth; const minCellDimension = screenWidth < 480 ? '35px' : (screenWidth < 768 ? '40px' : '45px'); const stdCols = screenWidth < 480 ? 8 : (screenWidth < 768 ? 10 : 16);
            boardElement.style.gridTemplateColumns = `repeat(${stdCols}, minmax(${minCellDimension}, 1fr))`;
            const numberCellsMap = new Map();
            BINGO_HEADERS.forEach(header => { const letterCell = document.createElement('div'); letterCell.className = 'board-cell board-letter'; letterCell.innerText = header; switch (header) { case 'B': letterCell.style.borderColor = 'var(--ln-red)'; break; case 'I': letterCell.style.borderColor = 'var(--ln-blue)'; break; case 'N': letterCell.style.borderColor = 'var(--ln-black)'; letterCell.style.borderWidth = '2px'; break; case 'G': letterCell.style.borderColor = 'var(--ln-green)'; break; case 'O': letterCell.style.borderColor = 'var(--ln-pink)'; break; } boardElement.appendChild(letterCell); const [min, max] = COLUMN_RANGES[header]; for (let num = min; num <= max; num++) { const numCell = document.createElement('div'); numCell.className = 'board-cell board-number'; numCell.innerText = num; numCell.id = `number-${num}`; if (calledNumbers.has(num)) numCell.classList.add('called'); numberCellsMap.set(num, numCell); boardElement.appendChild(numCell); } });
            boardElement.numberCellsMap = numberCellsMap; updateBoardHighlights();
        } else if (type === 'registration') {
            let currentRegRangeToUse; bodyElement.classList.add('registration-active');
            if (isInPreGameMode) { currentRegRangeToUse = preGameActiveRange; bodyElement.classList.add('pre-game-active'); boardElement.classList.add('pre-game-active-board-style'); }
            else if (activeRegistrationRange) { currentRegRangeToUse = activeRegistrationRange; bodyElement.classList.remove('pre-game-active'); boardElement.classList.add('registration-view'); }
            else { console.error("Registration layout called without range."); setBoardLayout('standard'); return; }
            const regCols = 20; const screenWidth = window.innerWidth; const minCellWidth = screenWidth < 480 ? '18px' : (screenWidth < 768 ? '22px' : '28px');
            boardElement.style.gridTemplateColumns = `repeat(${regCols}, minmax(${minCellWidth}, 1fr))`; boardElement.style.maxWidth = '98%';
            const [startNum, endNum] = currentRegRangeToUse === '1-100' ? [1, REGISTRATION_PAGE_SIZE] : [REGISTRATION_PAGE_SIZE + 1, TOTAL_CARDS];
            for (let i = startNum; i <= endNum; i++) { const cell = document.createElement('div'); cell.className = 'registration-number-cell'; cell.textContent = i; cell.dataset.cardNumber = i; if (registeredNumbers.has(i)) cell.classList.add('registered'); cell.addEventListener('click', handleRegistrationCellClick); boardElement.appendChild(cell); }
        }
    }

    function handleRegistrationCellClick(event) { if (isGameRunning || isShuffling) return; const cell = event.target.closest('.registration-number-cell'); if (!cell) return; const cardNumber = parseInt(cell.dataset.cardNumber, 10); if (isNaN(cardNumber) || cardNumber < 1 || cardNumber > TOTAL_CARDS) return; if (registeredNumbers.has(cardNumber)) { registeredNumbers.delete(cardNumber); cell.classList.remove('registered'); } else { registeredNumbers.add(cardNumber); cell.classList.add('registered'); } updatePlayerCountDisplay(); updateCardRegistrationMessages(); calculateBetting(currentStakePerPlayer); saveSettings(); }
    function updateBoardHighlights() { if (activeRegistrationRange || isInPreGameMode || !boardElement.numberCellsMap) return; const currentCustomColor = ['custom-green', 'custom-black', 'custom-blue'].find(cls => boardElement.classList.contains(cls)); if (currentCustomColor) { boardElement.classList.add(currentCustomColor); } else { boardElement.classList.remove('custom-green', 'custom-black', 'custom-blue'); } boardElement.numberCellsMap.forEach((cell, num) => { cell.classList.remove('called', 'shuffling', 'basic-win-board-highlight'); if (calledNumbers.has(num)) cell.classList.add('called'); }); }
    function updateLastCalledDisplays() { if (activeRegistrationRange || isInPreGameMode) { lastFiveWrapper.innerHTML = ''; lastTwoWrapper.innerHTML = ''; return; } lastFiveWrapper.innerHTML = ''; lastTwoWrapper.innerHTML = ''; const leftColors = ['ln-pink', 'ln-green', 'ln-blue', 'ln-yellow', 'ln-brown']; const lastFiveHistory = calledNumberHistory.slice(0, 5); lastFiveHistory.forEach((callInfo, index) => { const circle = document.createElement('div'); circle.className = 'last-number-circle'; circle.classList.add(leftColors[index % leftColors.length]); circle.textContent = `${callInfo.header}-${callInfo.number}`; lastFiveWrapper.appendChild(circle); }); const lastTwoHistory = calledNumberHistory.slice(0, 2); lastTwoHistory.forEach((callInfo) => { const circle = document.createElement('div'); circle.className = 'last-number-circle'; circle.textContent = `${callInfo.header}-${callInfo.number}`; lastTwoWrapper.appendChild(circle); }); }
    function customAlert(message, buttonsConfig = [{ text: 'OK', class: 'primary', callback: null }]) { customAlertMessage.innerHTML = message; customAlertOverlay.style.display = 'flex'; let currentChild = customAlertBox.lastChild; while (currentChild && currentChild !== customAlertMessage && currentChild.tagName === 'BUTTON') { customAlertBox.removeChild(currentChild); currentChild = customAlertBox.lastChild; } if (customAlertBox.firstChild !== customAlertMessage) { customAlertBox.insertBefore(customAlertMessage, customAlertBox.firstChild); } buttonsConfig.forEach(config => { const button = document.createElement('button'); button.textContent = config.text; button.className = `button ${config.class || 'primary'}`; button.onclick = () => { customAlertOverlay.style.display = 'none'; if (config.callback) config.callback(); }; customAlertBox.appendChild(button); }); const firstButton = customAlertBox.querySelector('button'); if (firstButton) { firstButton.focus(); } }
    function handleUserLockDecision(cardId, excludeCard) { const cardElement = cardElements.get(cardId); if (!cardElement) return; if (excludeCard) { cardStates.set(cardId, 'user-excluded'); if (winners.has(cardId)) winners.delete(cardId); setMessageOnCard(cardElement, 'BLOCKED', 'user-excluded-message'); playSound(audioElements.blockCardSound); if (cardElement.classList.contains('zoomed-card')) { handleUnzoom(cardElement); } } else { const currentState = cardStates.get(cardId); if (currentState !== 'winner' && currentState !== 'frozen' && currentState !== 'basic' && currentState !== 'user-excluded') { cardStates.set(cardId, 'normal'); } setMessageOnCard(cardElement, null, null); } updateSettingsUI(); saveSettings(); }
    function setMessageOnCard(cardElement, messageText, messageType) { if (!cardElement) return; let messageDiv = cardElement.querySelector('.card-message'); let exclusionPromptDiv = cardElement.querySelector('.card-exclusion-prompt'); if (!messageDiv) { messageDiv = document.createElement('div'); messageDiv.className = 'card-message'; cardElement.appendChild(messageDiv); } if (!exclusionPromptDiv) { exclusionPromptDiv = document.createElement('div'); exclusionPromptDiv.className = 'card-exclusion-prompt'; cardElement.appendChild(exclusionPromptDiv); } exclusionPromptDiv.style.display = 'none'; messageDiv.style.display = 'none'; messageDiv.className = 'card-message'; cardElement.classList.remove('awaiting-exclusion-decision', 'winner', 'locked', 'frozen', 'basic-winner'); if (messageType === 'prompt-exclusion') { exclusionPromptDiv.style.display = 'flex'; cardElement.classList.add('awaiting-exclusion-decision'); const promptMsgElement = exclusionPromptDiv.querySelector('.prompt-message'); if (promptMsgElement) { promptMsgElement.innerHTML = ""; promptMsgElement.style.display = 'none'; } } else if (messageText !== null && messageType) { let displayText = messageText; const promptMsgElement = exclusionPromptDiv.querySelector('.prompt-message'); if (promptMsgElement) { promptMsgElement.style.display = 'block'; } if (messageType === 'frozen-message') { displayText = 'No Winner'; cardElement.classList.add('frozen'); } else if (messageType === 'winner-message') { cardElement.classList.add('winner'); } else if (messageType === 'locked-message') { cardElement.classList.add('locked'); } else if (messageType === 'basic-winner-message') { cardElement.classList.add('basic-winner'); } if (['winner-message', 'not-winner-message', 'locked-message', 'frozen-message', 'basic-winner-message', 'user-excluded-message'].includes(messageType)) { messageDiv.classList.add(messageType); messageDiv.textContent = displayText; messageDiv.classList.add('visible'); messageDiv.style.display = 'block'; } } }
    function updateCardRegistrationMessages() { cardElements.forEach((cardElement) => { if (!cardElement) return; let regMsgDiv = cardElement.querySelector('.card-registration-message'); if (regMsgDiv) { regMsgDiv.textContent = ''; regMsgDiv.classList.remove('visible'); } }); }
    function evaluatePatterns(cardElement) { const size = 5; const cells = cardElement.cellElements; if (!cells || cells.length !== size || !cells[0] || cells[0].length !== size) { return { count: 0, completedCells: new Set() }; } const allMarked = list => list.every(cell => cell && cell.classList.contains('marked')); const completedCells = new Set(); let patternCount = 0; const completedLines = new Set(); for (let r = 0; r < size; r++) { if (allMarked(cells[r])) { const lineId = `row${r}`; if (!completedLines.has(lineId)) { patternCount++; completedLines.add(lineId); cells[r].forEach(cell => completedCells.add(cell)); } } } for (let c = 0; c < size; c++) { const colCells = []; for (let r = 0; r < size; r++) { colCells.push(cells[r][c]); } if (allMarked(colCells)) { const lineId = `col${c}`; if (!completedLines.has(lineId)) { patternCount++; completedLines.add(lineId); colCells.forEach(cell => completedCells.add(cell)); } } } const mainDiag = [], antiDiag = []; for (let i = 0; i < size; i++) { mainDiag.push(cells[i][i]); antiDiag.push(cells[i][size - 1 - i]); } if (allMarked(mainDiag)) { const lineId = 'diag0'; if (!completedLines.has(lineId)) { patternCount++; completedLines.add(lineId); mainDiag.forEach(cell => completedCells.add(cell)); } } if (allMarked(antiDiag)) { const lineId = 'diag1'; if (!completedLines.has(lineId)) { patternCount++; completedLines.add(lineId); antiDiag.forEach(cell => completedCells.add(cell)); } } const corners = [ cells[0][0], cells[0][size - 1], cells[size - 1][0], cells[size - 1][size - 1] ]; if (allMarked(corners)) { const lineId = 'corners'; if (!completedLines.has(lineId)) { patternCount++; completedLines.add(lineId); corners.forEach(cell => completedCells.add(cell)); } } return { count: patternCount, completedCells: completedCells }; }
    function updateCompletedVisuals(cardElement, evaluationResult) { if (!cardElement || !cardElement.cellElements) return; const size = 5; const cells = cardElement.cellElements; const completedCellsSet = evaluationResult.completedCells; for (let r = 0; r < size; r++) { for (let c = 0; c < 5; c++) { const cell = cells[r][c]; if (cell) { if (completedCellsSet.has(cell)) { cell.classList.add('completed'); } else { cell.classList.remove('completed'); } } } } }
    function generateBingoCard(cardId) { const card = document.createElement('div'); card.className = 'bingo-card'; card.id = `card${cardId}`; card.cellElements = Array(5).fill(null).map(() => Array(5).fill(null)); if (!cardStates.has(cardId)) { cardStates.set(cardId, 'normal'); } const cardHeader = document.createElement('div'); cardHeader.className = 'card-header'; cardHeader.innerText = `Card ${cardId}`; card.appendChild(cardHeader); card.addEventListener('dblclick', (event) => { if (activeRegistrationRange || isInPreGameMode) return; const currentCardState = cardStates.get(cardId); if (card.classList.contains('zoomed-card')) { if (card.classList.contains('awaiting-exclusion-decision')) { handleUserLockDecision(cardId, false); } handleUnzoom(card); } else { if (currentCardState === 'user-excluded') { customAlert(`Card ${cardId} is excluded.`); playSound(audioElements.errorSound); checkSpecificCard(cardId, true); return; } checkSpecificCard(cardId, true); } event.stopPropagation(); }); BINGO_HEADERS.forEach(header => { const hCell = document.createElement('div'); hCell.className = 'cell header'; hCell.innerText = header; card.appendChild(hCell); }); let cardNumbersGrid; if (fixedCardLayouts.has(cardId)) { cardNumbersGrid = fixedCardLayouts.get(cardId); } else { cardNumbersGrid = Array(5).fill(null).map(() => Array(5).fill(0)); BINGO_HEADERS.forEach((header, columnIndex) => { const [min, max] = COLUMN_RANGES[header]; const columnNumbers = generateDeterministicNumbers(columnIndex === 2 ? 4 : 5, min, max, cardId, columnIndex); let numIdx = 0; for (let r = 0; r < 5; r++) { if (r === 2 && columnIndex === 2) { cardNumbersGrid[r][columnIndex] = 'FREE'; } else { if (numIdx < columnNumbers.length) { cardNumbersGrid[r][columnIndex] = columnNumbers[numIdx++]; } else { cardNumbersGrid[r][columnIndex] = -1; } } } }); fixedCardLayouts.set(cardId, cardNumbersGrid); } cardLayouts.set(cardId, cardNumbersGrid); for (let r = 0; r < 5; r++) { for (let c = 0; c < 5; c++) { const cell = document.createElement('div'); cell.className = 'cell'; const number = cardNumbersGrid[r][c]; cell.textContent = (number === 'FREE' ? 'F' : number); cell.dataset.number = number; cell.dataset.row = r; cell.dataset.col = c; if (r === 2 && c === 2) { cell.classList.add('free', 'marked'); } else { if (registeredNumbers.has(cardId) && calledNumbers.has(number)) { cell.classList.add('marked'); } } card.appendChild(cell); card.cellElements[r][c] = cell; } } const messageDiv = document.createElement('div'); messageDiv.className = 'card-message'; card.appendChild(messageDiv); const exclusionPromptDiv = document.createElement('div'); exclusionPromptDiv.className = 'card-exclusion-prompt'; const promptMessageEl = document.createElement('p'); promptMessageEl.className = 'prompt-message'; exclusionPromptDiv.appendChild(promptMessageEl); const buttonContainer = document.createElement('div'); buttonContainer.className = 'prompt-buttons'; const excludeButton = document.createElement('button'); excludeButton.className = 'button danger prompt-button exclude'; excludeButton.textContent = 'Block Card'; excludeButton.addEventListener('click', (e) => { e.stopPropagation(); handleUserLockDecision(cardId, true); }); buttonContainer.appendChild(excludeButton); const keepButton = document.createElement('button'); keepButton.className = 'button primary prompt-button keep'; keepButton.textContent = 'Keep Active'; keepButton.addEventListener('click', (e) => { e.stopPropagation(); handleUserLockDecision(cardId, false); }); buttonContainer.appendChild(keepButton); exclusionPromptDiv.appendChild(buttonContainer); card.appendChild(exclusionPromptDiv); const cancelButton = document.createElement('button'); cancelButton.className = 'zoomed-cancel-button'; cancelButton.innerHTML = '<i class="fas fa-times"></i>'; cancelButton.setAttribute('aria-label', 'Close Card'); cancelButton.title = 'Close Card'; cancelButton.addEventListener('click', (e) => { e.stopPropagation(); if (card.classList.contains('awaiting-exclusion-decision')) { handleUserLockDecision(parseInt(card.id.replace('card',''), 10), false); } handleUnzoom(card); }); card.appendChild(cancelButton); cardElements.set(cardId, card); const currentState = cardStates.get(cardId); if (registeredNumbers.has(cardId)) { const initialEvaluation = evaluatePatterns(card); updateCompletedVisuals(card, initialEvaluation); if (currentState === 'winner') setMessageOnCard(card, 'Winner!', 'winner-message'); else if (currentState === 'locked') setMessageOnCard(card, `LOCKED (${initialEvaluation.count} patterns)`, 'locked-message'); else if (currentState === 'frozen') setMessageOnCard(card, 'No Winner', 'frozen-message'); else if (currentState === 'basic') setMessageOnCard(card, 'Basic Winner!', 'basic-winner-message'); else if (currentState === 'user-excluded') setMessageOnCard(card, 'BLOCKED', 'user-excluded-message'); else setMessageOnCard(card, null, null); } else { if (currentState === 'user-excluded') setMessageOnCard(card, 'BLOCKED', 'user-excluded-message'); else setMessageOnCard(card, null, null); } updateCardRegistrationMessages(); return card; }
    function createBingoCards() { cardsContainer.innerHTML = ''; cardElements.clear(); let layoutsLoaded = loadCardLayouts(); let layoutsGeneratedThisSession = false; for (let i = 1; i <= TOTAL_CARDS; i++) { if (!fixedCardLayouts.has(i)) { const cardElement = generateBingoCard(i); cardsContainer.appendChild(cardElement); layoutsGeneratedThisSession = true; } else { const cardElement = generateBingoCard(i); cardsContainer.appendChild(cardElement); } } if (layoutsGeneratedThisSession && !layoutsLoaded) { saveCardLayouts(); } cardElements.forEach((cardElement, cardId) => { const state = cardStates.get(cardId) || 'normal'; const isRegistered = registeredNumbers.has(cardId); const grid = cardLayouts.get(cardId); if (isRegistered && grid && cardElement.cellElements) { for (let r = 0; r < 5; r++) { for (let c = 0; c < 5; c++) { const cell = cardElement.cellElements[r][c]; if (cell) { const number = grid[r][c]; if (r === 2 && c === 2) { cell.classList.add('marked'); } else if (number !== 'FREE' && calledNumbers.has(number)) { cell.classList.add('marked'); } else { cell.classList.remove('marked'); } cell.classList.remove('completed'); } } } const evaluation = evaluatePatterns(cardElement); updateCompletedVisuals(cardElement, evaluation); if (state === 'winner') setMessageOnCard(cardElement, 'Winner!', 'winner-message'); else if (state === 'locked') setMessageOnCard(cardElement, `LOCKED (${evaluation.count} patterns)`, 'locked-message'); else if (state === 'frozen') setMessageOnCard(cardElement, 'No Winner', 'frozen-message'); else if (state === 'basic') setMessageOnCard(cardElement, 'Basic Winner!', 'basic-winner-message'); else if (state === 'user-excluded') setMessageOnCard(cardElement, 'BLOCKED', 'user-excluded-message'); else setMessageOnCard(cardElement, null, null); } else { if (state === 'user-excluded') setMessageOnCard(cardElement, 'BLOCKED', 'user-excluded-message'); else setMessageOnCard(cardElement, null, null); } updateCardRegistrationMessages(); }); }
    function highlightBasicWinNumbersOnBoard(cardId) { if (activeRegistrationRange || isInPreGameMode || !boardElement.numberCellsMap || !cardLayouts.has(cardId)) return; clearBasicWinBoardHighlights(); const cardGrid = cardLayouts.get(cardId); for (let r = 0; r < 5; r++) { for (let c = 0; c < 5; c++) { const number = cardGrid[r][c]; if (number !== 'FREE' && typeof number === 'number' && number > 0) { const boardCell = boardElement.numberCellsMap.get(number); if (boardCell) boardCell.classList.add('basic-win-board-highlight'); } } } }
    function clearBasicWinBoardHighlights() { if (activeRegistrationRange || isInPreGameMode || !boardElement.numberCellsMap) return; boardElement.numberCellsMap.forEach(cell => cell.classList.remove('basic-win-board-highlight'));}
    function callNumber() { if (isShuffling || !isGameRunning || activeRegistrationRange || isInPreGameMode) return; clearBasicWinBoardHighlights(); let numToCall = null, hdrForNum = null; if (currentShuffleNumbers.length > 0) { const availableNumbers = currentShuffleNumbers.filter(item => !calledNumbers.has(item.number)); if (availableNumbers.length > 0) { [numToCall, hdrForNum] = [availableNumbers[0].number, availableNumbers[0].header]; const indexToRemove = currentShuffleNumbers.findIndex(item => item.number === numToCall); if (indexToRemove > -1) currentShuffleNumbers.splice(indexToRemove, 1); } else { currentShuffleNumbers = []; } } if (numToCall === null) { const remaining = Array.from({length: 75}, (_, i) => i + 1).filter(n => !calledNumbers.has(n)); if (remaining.length === 0) { pauseGame("Completed (All Called)"); customAlert("All numbers have been called!"); isGameRunning = false; updateSettingsUI(); return; } numToCall = remaining[Math.floor(Math.random() * remaining.length)]; for (const [h, [minR, maxR]] of Object.entries(COLUMN_RANGES)) { if (numToCall >= minR && numToCall <= maxR) { hdrForNum = h; break; } } } if (numToCall !== null && hdrForNum !== null) { callCount++; updateCallCountDisplay(); lastCalledInfo = { number: numToCall, header: hdrForNum, callIndex: callCount }; calledNumbers.add(numToCall); calledNumberHistory.unshift(lastCalledInfo); const displayNumber = `${hdrForNum}-${numToCall}`; calledNumberDisplay.innerText = displayNumber; updateLastCalledDisplays(); const boardCell = boardElement.numberCellsMap?.get(numToCall); if (boardCell) boardCell.classList.add('called'); registeredNumbers.forEach(cardId => { const cardElement = cardElements.get(cardId); const cardState = cardStates.get(cardId); if (!cardElement || !cardElement.cellElements || cardState === 'user-excluded') { return; } const grid = cardLayouts.get(cardId); let cardWasMarkedThisCall = false; if (grid && grid.flat().includes(numToCall)) { for (let r = 0; r < 5; r++) { for (let c = 0; c < 5; c++) { if (grid[r][c] == numToCall) { const cell = cardElement.cellElements[r][c]; if (cell && !cell.classList.contains('free') && !cell.classList.contains('marked')) { cell.classList.add('marked'); cardWasMarkedThisCall = true; } } } } } if (cardWasMarkedThisCall) { const currentEvaluation = evaluatePatterns(cardElement); updateCompletedVisuals(cardElement, currentEvaluation); } if (callCount === BASIC_WIN_CALL_COUNT && cardState === 'normal') { let markedCountExcludingFree = 0; if (cardElement.cellElements) { for (let r = 0; r < 5; r++) { for (let c = 0; c < 5; c++) { const cell = cardElement.cellElements[r][c]; if (cell && cell.classList.contains('marked') && !(r === 2 && c === 2)) markedCountExcludingFree++; }}} if (markedCountExcludingFree === 0) { cardStates.set(cardId, 'basic'); winners.add(cardId); setMessageOnCard(cardElement, 'Basic Winner!', 'basic-winner-message'); playSound(audioElements.basicWinSound); } } }); playNumberSound(hdrForNum, numToCall); } else if (isGameRunning) { pauseGame("Error determining next number. Game stopped."); } updateSettingsUI(); saveSettings(); }
    function checkSpecificCard(cardId, performZoomIntent = true) { if (activeRegistrationRange || isInPreGameMode) return; const cardElement = cardElements.get(cardId); if (!cardElement) { customAlert("Card " + cardId + " not found."); playSound(audioElements.errorSound); return; } const isRegistered = registeredNumbers.has(cardId); if (!isRegistered) { customAlert("Card " + cardId + " is not registered."); playSound(audioElements.errorSound); if (cardElement.classList.contains('zoomed-card')) { handleUnzoom(cardElement); } return; } const cardStateBeforeCheck = cardStates.get(cardId) || 'normal'; let cardWasJustZoomed = false; if (performZoomIntent) { const currentlyZoomed = document.querySelector('.bingo-card.zoomed-card'); if (currentlyZoomed && currentlyZoomed !== cardElement) { handleUnzoom(currentlyZoomed); } if (!cardElement.classList.contains('zoomed-card')) { cardElement.classList.add('zoomed-card'); cardWasJustZoomed = true; } } if (cardStateBeforeCheck === 'user-excluded') { setMessageOnCard(cardElement, 'BLOCKED', 'user-excluded-message'); return; } clearBasicWinBoardHighlights(); const currentEvaluation = evaluatePatterns(cardElement); const patternCount = currentEvaluation.count; updateCompletedVisuals(cardElement, currentEvaluation); if (cardStateBeforeCheck === 'basic' || cardStates.get(cardId) === 'basic') { setMessageOnCard(cardElement, 'Basic Winner!', 'basic-winner-message'); if (!winners.has(cardId)) winners.add(cardId); playSound(audioElements.basicWinSound); highlightBasicWinNumbersOnBoard(cardId); } else { if (callCount === BASIC_WIN_CALL_COUNT && cardStateBeforeCheck === 'normal') { let markedCountExcludingFree = 0; if (cardElement.cellElements) { for (let r = 0; r < 5; r++) { for (let c = 0; c < 5; c++) { const cell = cardElement.cellElements[r][c]; if (cell && cell.classList.contains('marked') && !(r === 2 && c === 2)) markedCountExcludingFree++; }}} if (markedCountExcludingFree === 0) { cardStates.set(cardId, 'basic'); setMessageOnCard(cardElement, 'Basic Winner!', 'basic-winner-message'); if (!winners.has(cardId)) winners.add(cardId); playSound(audioElements.basicWinSound); highlightBasicWinNumbersOnBoard(cardId); saveSettings(); return; } } if (cardStates.get(cardId) !== 'basic') { if (patternCount < requiredPatternCount) { if (cardWasJustZoomed) { setMessageOnCard(cardElement, null, 'prompt-exclusion'); } else { if (cardStates.get(cardId) !== 'user-excluded') { cardStates.set(cardId, 'locked'); if (winners.has(cardId)) winners.delete(cardId); setMessageOnCard(cardElement, `LOCKED (${patternCount} patterns)`, 'locked-message'); playSound(audioElements.lockedSound); } } } else { const lastNumberCalled = lastCalledInfo ? lastCalledInfo.number : null; if (!lastCalledInfo || callCount === 0) { cardStates.set(cardId, 'locked'); if (winners.has(cardId)) winners.delete(cardId); setMessageOnCard(cardElement, `LOCKED (No calls yet)`, 'locked-message'); playSound(audioElements.lockedSound); } else { let lastCallIsARedCellInCompletedPattern = false; if (currentEvaluation.completedCells && currentEvaluation.completedCells.size > 0) { for (const cell of currentEvaluation.completedCells) { if (parseInt(cell.dataset.number, 10) === lastNumberCalled) { lastCallIsARedCellInCompletedPattern = true; break; } } } if (lastCallIsARedCellInCompletedPattern) { const wasPreviouslyWinner = (cardStateBeforeCheck === 'winner'); cardStates.set(cardId, 'winner'); if (!winners.has(cardId)) winners.add(cardId); setMessageOnCard(cardElement, 'Winner!', 'winner-message'); if (!wasPreviouslyWinner) { playSound(audioElements.winnerSound); createConfetti(); } } else { cardStates.set(cardId, 'frozen'); if (winners.has(cardId)) winners.delete(cardId); setMessageOnCard(cardElement, 'No Winner', 'frozen-message'); playSound(audioElements.frozenSound); } } } } } saveSettings(); }

    function resetGame() {
        if (isGameRunning) pauseGame("Resetting");
        stopShuffling();
        calledNumbers.clear();
        calledNumberHistory.length = 0;
        currentShuffleNumbers.length = 0;
        winners.clear();
        cardStates.clear();
        cardElements.forEach((cardElement, cardId) => {
            setMessageOnCard(cardElement, null, null);
            updateCardRegistrationMessages();
            if (cardElement.cellElements) {
                for (let r = 0; r < 5; r++) {
                    for (let c = 0; c < 5; c++) {
                        const cell = cardElement.cellElements[r][c];
                        if (cell) {
                            if (!(r === 2 && c === 2)) {
                                cell.classList.remove('marked', 'completed');
                            } else {
                                cell.classList.add('marked');
                                cell.classList.remove('completed');
                            }
                        }
                    }
                }
            }
            cardElement.classList.remove('winner', 'locked', 'frozen', 'basic-winner', 'awaiting-exclusion-decision');
        });
        for (let i = 1; i <= TOTAL_CARDS; i++) {
            cardStates.set(i, 'normal');
        }
        callCount = 0;
        lastCalledInfo = null;
        // registeredNumbers.clear(); // MODIFIED: This line is now removed/commented out
        if (calledNumberDisplay) calledNumberDisplay.innerText = '--';
        updateLastCalledDisplays();
        updateCallCountDisplay();
        updatePlayerCountDisplay(); // This will now reflect the persisted registered numbers
        if (winnerSearchInput) winnerSearchInput.value = '';
        const zoomedCard = document.querySelector('.bingo-card.zoomed-card');
        if (zoomedCard) {
            handleUnzoom(zoomedCard);
        }
        clearBasicWinBoardHighlights();
        isInPreGameMode = true;
        activeRegistrationRange = null;
        preGameActiveRange = '1-100';
        playSound(audioElements.resetSound);
        enterPreGameRegistrationView(); // This will show the persisted registered numbers on the board
        calculateBetting(currentStakePerPlayer); // Betting will be calculated based on persisted registered numbers
        saveSettings(); // Settings will be saved with persisted registered numbers
        updateSettingsUI();
    }

    function enterPreGameRegistrationView() { if (!isInPreGameMode) return; setBoardLayout('registration'); if (preGameRegNav1_100) preGameRegNav1_100.classList.toggle('active', preGameActiveRange === '1-100'); if (preGameRegNav101_200) preGameRegNav101_200.classList.toggle('active', preGameActiveRange === '101-200'); updateCardRegistrationMessages(); updatePlayerCountDisplay(); updateSettingsUI(); }
    function clearAllPreGameRegistrations() { if (!isInPreGameMode) return; if (registeredNumbers.size > 0) { registeredNumbers.clear(); updatePlayerCountDisplay(); enterPreGameRegistrationView(); updateCardRegistrationMessages(); calculateBetting(currentStakePerPlayer); saveSettings(); } }
    function toggleRegistrationView(range) { if (isGameRunning || isShuffling || isInPreGameMode) { customAlert("Cannot change view now."); return; } const zoomedCard = document.querySelector('.bingo-card.zoomed-card'); if (zoomedCard) handleUnzoom(zoomedCard); clearBasicWinBoardHighlights(); if (activeRegistrationRange === range) { activeRegistrationRange = null; setBoardLayout('standard'); } else { activeRegistrationRange = range; setBoardLayout('registration'); } updateSettingsUI(); }
    function startGame() { if (isGameRunning || isShuffling || activeRegistrationRange || isInPreGameMode) return; if (callCount === 0) { if (registeredNumbers.size > 0 && currentFee > 0) { if (walletBalance < currentFee) { customAlert(`Insufficient balance (${walletBalance.toFixed(0)}) for fee (${currentFee.toFixed(0)}).`); playSound(audioElements.errorSound); return; } const gameCountIncrement = registeredNumbers.size <= 5 ? 1 : 1.5; totalGamesPlayed += gameCountIncrement; dailyGamesPlayed += 1; dailyEarnings += currentFee; totalEarnings += currentFee; walletBalance -= currentFee; } else if (registeredNumbers.size > 0 && currentFee === 0) { const gameCountIncrement = 1; totalGamesPlayed += gameCountIncrement; dailyGamesPlayed += 1; } } isGameRunning = true; playSound(audioElements.startSound); updateStatsDisplay(); updateSettingsUI(); saveSettings(); setTimeout(() => { if (!isGameRunning) return; callNumber(); if (isGameRunning) { intervalId = setInterval(callNumber, callSpeed); } }, 2000); }
    function pauseGame(reason = "Paused") { if (!isGameRunning) return; isGameRunning = false; clearInterval(intervalId); intervalId = null; playSound(audioElements.pauseSound); updateSettingsUI(); console.log(`Game ${reason}.`); }
    
    /**
     * Shuffles an array in place using the Fisher-Yates algorithm.
     * @param {Array} array The array to shuffle.
     * @returns {Array} The shuffled array.
     */
    function fisherYatesShuffle(array) {
        let currentIndex = array.length, randomIndex;
        // While there remain elements to shuffle.
        while (currentIndex !== 0) {
            // Pick a remaining element.
            randomIndex = Math.floor(Math.random() * currentIndex);
            currentIndex--;
            // And swap it with the current element.
            [array[currentIndex], array[randomIndex]] = [
                array[randomIndex], array[currentIndex]];
        }
        return array;
    }

    function startShuffling() {
        if (isShuffling || isGameRunning || activeRegistrationRange || isInPreGameMode) return;
        isShuffling = true;
        clearBasicWinBoardHighlights();
        shuffleDisplayElement.style.display = 'block';
        updateSettingsUI();
        playSound(audioElements.shuffleSound);

        const avail = Array.from({length: 75}, (_, i) => i + 1).filter(n => !calledNumbers.has(n));
        if (avail.length === 0) {
            stopShuffling();
            customAlert("No numbers remaining to shuffle.");
            return;
        }

        // Prepare the sequence for when shuffling stops (if game starts)
        let itemsToShuffleForCallSequence = avail.map(n => {
            let h = '';
            for (const [hdr, [min, max]] of Object.entries(COLUMN_RANGES)) {
                if (n >= min && n <= max) {
                    h = hdr;
                    break;
                }
            }
            return { number: n, header: h };
        });
        currentShuffleNumbers = fisherYatesShuffle(itemsToShuffleForCallSequence);

        if (shuffleIntervalId) clearInterval(shuffleIntervalId);
        
        let lastAnimatedBoardCells = []; // Stores DOM elements of cells animated in the previous tick

        shuffleIntervalId = setInterval(() => {
            if (!isShuffling) { // Check if shuffling was stopped externally
                clearInterval(shuffleIntervalId);
                // Ensure all shuffling classes are removed from the board
                boardElement.numberCellsMap?.forEach(cell => cell.classList.remove('shuffling'));
                lastAnimatedBoardCells = []; // Clear the tracking array
                return;
            }

            // 1. Clear previous shuffling classes
            lastAnimatedBoardCells.forEach(cell => {
                if (cell) cell.classList.remove('shuffling');
            });
            lastAnimatedBoardCells = []; // Reset for the current tick

            const numberOfCellsToAnimate = 5; // How many numbers to animate on the board at once
            const cellsToAnimateThisTick = []; // Will store DOM elements for current tick's animation

            if (avail.length > 0) {
                // Create a temporary shuffled copy of available numbers to pick from for this tick's animation
                const shuffledAvailForTick = [...avail]; // Copy avail
                fisherYatesShuffle(shuffledAvailForTick); // Shuffle the copy

                for (let i = 0; i < Math.min(numberOfCellsToAnimate, shuffledAvailForTick.length); i++) {
                    const numToAnimate = shuffledAvailForTick[i];
                    const boardCell = boardElement.numberCellsMap?.get(numToAnimate);
                    if (boardCell && !boardCell.classList.contains('called')) {
                        boardCell.classList.add('shuffling');
                        cellsToAnimateThisTick.push(boardCell); // Store the DOM element
                    }
                }
                
                // Update the central display with one of the animated numbers (or a generic message)
                if (cellsToAnimateThisTick.length > 0) {
                    // Pick a random cell from the ones actually animated this tick
                    const randomAnimatedCell = cellsToAnimateThisTick[Math.floor(Math.random() * cellsToAnimateThisTick.length)];
                    const randomAnimatedNum = parseInt(randomAnimatedCell.innerText, 10); // Get number from cell's text
                    
                    let displayHdr = '';
                    for (const [hdr, [min, max]] of Object.entries(COLUMN_RANGES)) {
                        if (randomAnimatedNum >= min && randomAnimatedNum <= max) {
                            displayHdr = hdr;
                            break;
                        }
                    }
                    shuffleDisplayElement.textContent = `${displayHdr}-${randomAnimatedNum}`;
                } else if (avail.length > 0) { 
                    shuffleDisplayElement.textContent = "Shuffling...";
                } else { 
                    shuffleDisplayElement.textContent = "No Numbers";
                }

            } else { 
                shuffleDisplayElement.textContent = "No Numbers";
            }
            
            lastAnimatedBoardCells = cellsToAnimateThisTick; // Store for cleanup in the next tick

        }, 150); // Interval time in milliseconds (e.g., 150ms)
    }

    function stopShuffling() {
        if (!isShuffling) return;
        isShuffling = false; 
        clearInterval(shuffleIntervalId); 
        shuffleIntervalId = null;
        if (audioElements.shuffleSound) { 
            audioElements.shuffleSound.pause(); 
            audioElements.shuffleSound.currentTime = 0; 
        }
        playSound(audioElements.shuffleStopSound);
        clearTimeout(shuffleDisplayTimeout); 
        shuffleDisplayTimeout = setTimeout(() => { 
            shuffleDisplayElement.style.display = 'none'; 
        }, 1500);
        boardElement.numberCellsMap?.forEach(cell => cell.classList.remove('shuffling')); // Comprehensive cleanup
        updateSettingsUI(); 
        const displayStatus = calledNumberHistory.length > 0 ? `${calledNumberHistory[0].header}-${calledNumberHistory[0].number}` : '--'; 
        calledNumberDisplay.innerText = displayStatus; 
    }

    function updateSettingsUI() {
        updatePlayerCountDisplay(); updateSpeedDisplay(); updateCallCountDisplay();
        const isRegularRegViewActive = activeRegistrationRange !== null;
        const isRegistrationActive = isRegularRegViewActive || isInPreGameMode;

        bodyElement.classList.toggle('pre-game-active', isInPreGameMode);
        bodyElement.classList.toggle('registration-active', isRegistrationActive);

        if (preGameControlsContainer) { preGameControlsContainer.style.display = isInPreGameMode ? 'flex' : 'none'; }
        if (preGameStartButton) preGameStartButton.disabled = !isInPreGameMode;
        if (preGameClearRegistrationsButton) preGameClearRegistrationsButton.disabled = !isInPreGameMode;
        if (boardElement) { boardElement.style.display = 'grid'; }

        const canEnterRegularRegMode = !isGameRunning && !isShuffling && !isInPreGameMode;
        if (regNavControls) { regNavControls.style.display = (canEnterRegularRegMode || isRegularRegViewActive) ? 'flex' : 'none'; }
        if (regNavButton1_100) { regNavButton1_100.disabled = !canEnterRegularRegMode && !isRegularRegViewActive; regNavButton1_100.classList.toggle('active', isRegularRegViewActive && activeRegistrationRange === '1-100'); }
        if (regNavButton101_200) { regNavButton101_200.disabled = !canEnterRegularRegMode && !isRegularRegViewActive; regNavButton101_200.classList.toggle('active', isRegularRegViewActive && activeRegistrationRange === '101-200'); }

        const disableWhenGameActiveOrReg = isGameRunning || isShuffling || isRegistrationActive;
        if(startButton) { startButton.disabled = disableWhenGameActiveOrReg; if (isGameRunning) startButton.textContent = 'Game Running'; else if (calledNumbers.size > 0 && !isRegistrationActive) startButton.textContent = 'Resume Game'; else startButton.textContent = 'Start Game'; }
        if(pauseButton) pauseButton.disabled = !isGameRunning || isRegistrationActive;
        if(resetButton) resetButton.disabled = isGameRunning || isShuffling;
        if(shuffleButton) shuffleButton.disabled = disableWhenGameActiveOrReg;
        if(stopShuffleButton) stopShuffleButton.style.display = isShuffling && !isRegistrationActive ? 'inline-block' : 'none';
        if(stopShuffleButton) stopShuffleButton.disabled = !isShuffling;
        if(winnerSearchInput) winnerSearchInput.disabled = isRegistrationActive;
        if(winnerSearchButton) winnerSearchButton.disabled = isRegistrationActive;

        const disableSpeedControls = isShuffling || isRegistrationActive;
        if(speedDecreaseButton) speedDecreaseButton.disabled = disableSpeedControls;
        if(speedIncreaseButton) speedIncreaseButton.disabled = disableSpeedControls;

        if(volumeControl) volumeControl.disabled = isRegistrationActive;
        if(requiredPatternsSelect) requiredPatternsSelect.disabled = disableWhenGameActiveOrReg;
        if(stakePerPlayerInput) stakePerPlayerInput.disabled = disableWhenGameActiveOrReg;
        if(setStakeButton) setStakeButton.disabled = disableWhenGameActiveOrReg || registeredNumbers.size === 0;
        if (setBalanceInput) setBalanceInput.disabled = disableWhenGameActiveOrReg; // Added
        if (setBalanceButton) setBalanceButton.disabled = disableWhenGameActiveOrReg; // Added


        const hideBoardControls = isRegistrationActive;
        const boardSubControls = document.getElementById('board-sub-controls'); if(boardSubControls) boardSubControls.style.display = hideBoardControls ? 'none' : 'flex';
        const boardAttachedColorControls = document.getElementById('board-attached-color-controls'); if (boardAttachedColorControls) boardAttachedColorControls.style.display = hideBoardControls ? 'none' : 'flex';
        if(actionManualCall) actionManualCall.disabled = isGameRunning || isShuffling || isRegistrationActive || calledNumbers.size >= 75;
        if(actionReannounce) actionReannounce.disabled = isShuffling || isRegistrationActive || !lastCalledInfo;
        if(actionFindNumBoard) actionFindNumBoard.disabled = isShuffling || isRegistrationActive || !boardElement.numberCellsMap;
        if(actionQuickRules) actionQuickRules.disabled = isShuffling || isRegistrationActive;
        if (backToGameBoardButton && backToGameBoardButton.parentElement) { backToGameBoardButton.parentElement.style.display = (isRegularRegViewActive && !isInPreGameMode) ? 'flex' : 'none'; }
    }

    function setupEventListeners() {
        volumeControl.addEventListener('input', () => { const vol = volumeControl.value; Object.values(audioElements).forEach(a => { if(a) a.volume = vol; }); });
        themeToggle.addEventListener('click', () => { document.body.classList.toggle('light-theme'); themeToggle.textContent = document.body.classList.contains('light-theme') ? '🌙' : '☀️'; saveSettings(); });
        speedDecreaseButton.addEventListener('click', () => { if (activeRegistrationRange || isInPreGameMode ) return; callSpeed = Math.min(MAX_SPEED, callSpeed + SPEED_INCREMENT); updateSpeedDisplay(); saveSettings(); if (isGameRunning && !isShuffling && intervalId) { clearInterval(intervalId); intervalId = setInterval(callNumber, callSpeed); } });
        speedIncreaseButton.addEventListener('click', () => { if (activeRegistrationRange || isInPreGameMode) return; callSpeed = Math.max(MIN_SPEED, callSpeed - SPEED_INCREMENT); updateSpeedDisplay(); saveSettings(); if (isGameRunning && !isShuffling && intervalId) { clearInterval(intervalId); intervalId = setInterval(callNumber, callSpeed); } });
        startButton.addEventListener('click', () => { if (isGameRunning) { pauseGame("Paused from Start/Resume Button"); } else { startGame(); } });
        pauseButton.addEventListener('click', () => pauseGame("Paused from Pause Button"));
        resetButton.addEventListener('click', resetGame);
        shuffleButton.addEventListener('click', startShuffling);
        stopShuffleButton.addEventListener('click', stopShuffling);
        regNavButton1_100.addEventListener('click', () => toggleRegistrationView('1-100'));
        regNavButton101_200.addEventListener('click', () => toggleRegistrationView('101-200'));
        setStakeButton.addEventListener('click', () => { if (isGameRunning || isShuffling || activeRegistrationRange || isInPreGameMode) { customAlert("Cannot set stake now."); return; } if (registeredNumbers.size === 0) { customAlert("Register cards first to set stake."); playSound(audioElements.errorSound); return; } const stakeValue = parseInt(stakePerPlayerInput.value, 10); if (isNaN(stakeValue) || stakeValue < 10 || stakeValue % 10 !== 0) { customAlert("Invalid stake (>=10, increments of 10)."); playSound(audioElements.errorSound); stakePerPlayerInput.focus(); return; } calculateBetting(stakeValue); customAlert(`Stake set to ${stakeValue} ETB/player. Fee: ${currentFee.toFixed(0)}, Derash: ${currentDerash.toFixed(0)}. Ready.`); });
        winnerSearchButton.addEventListener('click', () => { if (activeRegistrationRange || isInPreGameMode) return; const cardNumToCheck = parseInt(winnerSearchInput.value, 10); if (isNaN(cardNumToCheck) || cardNumToCheck < 1 || cardNumToCheck > TOTAL_CARDS) { customAlert(`Invalid card number (1-${TOTAL_CARDS}).`); playSound(audioElements.errorSound); winnerSearchInput.focus(); winnerSearchInput.select(); return; } checkSpecificCard(cardNumToCheck, true); winnerSearchInput.select(); });
        winnerSearchInput.addEventListener('keypress', (e) => { if (e.key === 'Enter') { winnerSearchButton.click(); } });
        requiredPatternsSelect.addEventListener('change', (event) => { if (isGameRunning || activeRegistrationRange || isInPreGameMode) return; requiredPatternCount = parseInt(event.target.value, 10); saveSettings(); });
        document.addEventListener('click', function(event) { if (activeRegistrationRange || isInPreGameMode) return; const zoomedCard = document.querySelector('.bingo-card.zoomed-card'); if (zoomedCard && !event.target.closest('.zoomed-card') && !event.target.closest('#winner-search-button') && !event.target.closest('#custom-alert-box') && !event.target.closest('.zoomed-cancel-button') && !zoomedCard.classList.contains('awaiting-exclusion-decision')) { handleUnzoom(zoomedCard); } });
        document.addEventListener('keydown', (e) => { if (e.key === 'Escape') { if (customAlertOverlay.style.display === 'flex') { const currentFirstAlertButton = customAlertBox.querySelector('button'); if (currentFirstAlertButton) { currentFirstAlertButton.click(); } else { customAlertOverlay.style.display = 'none';} } else { const zoomedCard = document.querySelector('.bingo-card.zoomed-card'); if (zoomedCard) { if (zoomedCard.classList.contains('awaiting-exclusion-decision')) { handleUserLockDecision(parseInt(zoomedCard.id.replace('card',''), 10), false); } handleUnzoom(zoomedCard); } else if (activeRegistrationRange) { toggleRegistrationView(activeRegistrationRange); } } } });
        if (actionManualCall) { actionManualCall.addEventListener('click', () => { if (isGameRunning) { customAlert("Pause game to use Manual Call."); return; } if (isShuffling || activeRegistrationRange || isInPreGameMode) { customAlert("Cannot manually call now."); return; } if (calledNumbers.size >= 75) { customAlert("All numbers have been called."); return; } if (callCount === 0 && registeredNumbers.size > 0) { if (currentFee > 0 && walletBalance < currentFee) { customAlert(`Insufficient balance (${walletBalance.toFixed(0)}) for fee (${currentFee.toFixed(0)}). Cannot start.`); playSound(audioElements.errorSound); return; } if (currentFee > 0) { const gameCountIncrement = registeredNumbers.size <= 5 ? 1 : 1.5; totalGamesPlayed += gameCountIncrement; dailyGamesPlayed += 1; dailyEarnings += currentFee; totalEarnings += currentFee; walletBalance -= currentFee; } else { const gameCountIncrement = 1; totalGamesPlayed += gameCountIncrement; dailyGamesPlayed += 1; } updateStatsDisplay(); saveSettings(); } const gameWasInitiallyRunning = isGameRunning; isGameRunning = true; callNumber(); isGameRunning = gameWasInitiallyRunning; updateSettingsUI(); }); }
        if (actionReannounce) { actionReannounce.addEventListener('click', () => { if (lastCalledInfo && lastCalledInfo.header && lastCalledInfo.number) { playNumberSound(lastCalledInfo.header, lastCalledInfo.number); } else { customAlert("No number has been called yet."); } }); }
        if (actionFindNumBoard) { actionFindNumBoard.addEventListener('click', () => { if (activeRegistrationRange || isInPreGameMode || !boardElement.numberCellsMap) { customAlert("Board not in correct view to find number."); return; } const numToFind = prompt("Enter number to find on the board (1-75):"); if (numToFind) { const num = parseInt(numToFind, 10); if (!isNaN(num) && num >= 1 && num <= 75) { clearBasicWinBoardHighlights(); const cell = boardElement.numberCellsMap.get(num); if (cell) { cell.scrollIntoView({ behavior: 'smooth', block: 'center' }); cell.classList.add('basic-win-board-highlight'); setTimeout(() => cell.classList.remove('basic-win-board-highlight'), 3000); } else { customAlert("Number " + num + " somehow not on board map."); } } else { customAlert("Invalid number. Please enter 1-75."); } } }); }
        if (actionQuickRules) { actionQuickRules.addEventListener('click', () => { const rulesText = `Game Rules:\n1. Set stake & register cards.\n2. Start Game: Numbers called automatically.\n3. Patterns: ${requiredPatternCount} full lines (rows, cols, diags, 4 corners) for a win.\n4. Basic Win: 0 marked numbers (excl. FREE) after ${BASIC_WIN_CALL_COUNT} calls.\n5. Check Card: Dbl-click or use 'Check Card' button.\n   - Winner: Met pattern count AND last called number is part of a completed pattern (is a "red cell").\n   - Locked: Not enough patterns (system state) OR card excluded by user.\n   - No Winner: Met pattern count BUT last called number is NOT part of a completed pattern.\n   - User Excluded: Card manually removed from play via prompt after checking with insufficient patterns.\n6. Registration: Use 'Cards 1-100/101-200' buttons (game stopped).\nFee: ${FEE_PERCENTAGE}% of total stake (if > 5 players). Derash = Total - Fee.`; customAlert(rulesText); }); }
        if (preGameStartButton) { preGameStartButton.addEventListener('click', () => { isInPreGameMode = false; activeRegistrationRange = null; setBoardLayout('standard'); startGame(); updateSettingsUI(); }); }
        if (preGameClearRegistrationsButton) { preGameClearRegistrationsButton.addEventListener('click', clearAllPreGameRegistrations); }
        if (preGameRegNav1_100) { preGameRegNav1_100.addEventListener('click', () => { if (isInPreGameMode) { preGameActiveRange = '1-100'; enterPreGameRegistrationView(); } }); }
        if (preGameRegNav101_200) { preGameRegNav101_200.addEventListener('click', () => { if (isInPreGameMode) { preGameActiveRange = '101-200'; enterPreGameRegistrationView(); } }); }
        if (backToGameBoardButton) { backToGameBoardButton.addEventListener('click', () => { if (isInPreGameMode || activeRegistrationRange === null) { return; } const zoomedCard = document.querySelector('.bingo-card.zoomed-card'); if (zoomedCard) { handleUnzoom(zoomedCard); } clearBasicWinBoardHighlights(); activeRegistrationRange = null; setBoardLayout('standard'); updateSettingsUI(); }); }
        if (customAlertOkButton) { customAlertOkButton.addEventListener('click', () => { customAlertOverlay.style.display = 'none'; }); }

        // Event Listener for Set Balance Button
        if (setBalanceButton) {
            setBalanceButton.addEventListener('click', () => {
                if (isGameRunning || isShuffling || activeRegistrationRange || isInPreGameMode) {
                    customAlert("Cannot set balance while game is active or during registration.");
                    playSound(audioElements.errorSound);
                    return;
                }

                const balanceValueStr = setBalanceInput.value;
                const newBalance = parseFloat(balanceValueStr);

                // Check if NaN or negative
                if (isNaN(newBalance) || newBalance < 0) {
                    customAlert(`Invalid balance amount. Please enter a non-negative number.`);
                    playSound(audioElements.errorSound);
                    setBalanceInput.focus();
                    setBalanceInput.select();
                    return;
                }

                walletBalance = newBalance;
                updateStatsDisplay();
                saveSettings();
                setBalanceInput.value = '';
                customAlert(`Wallet balance set to ${walletBalance.toLocaleString()}.`);
                playSound(audioElements.startSound);
            });
        }
    }

    window.addEventListener('load', () => {
        isInPreGameMode = false; activeRegistrationRange = null;
        loadSettings(); createBingoCards(); setupEventListeners();
        isGameRunning = false; isShuffling = false; if(stopShuffleButton) stopShuffleButton.style.display = 'none';
        if(customAlertOverlay) customAlertOverlay.style.display = 'none';
        const initialVolume = parseFloat(volumeControl.value); Object.values(audioElements).forEach(audio => { if(audio) audio.volume = initialVolume; });
        if(calledNumberDisplay) calledNumberDisplay.innerText = '--'; updateLastCalledDisplays();
        if(winnerSearchInput) winnerSearchInput.max = TOTAL_CARDS;

        if (cardsContainer) { // Ensure container is hidden on load
            cardsContainer.classList.add('cards-hidden');
        }

        calculateBetting(currentStakePerPlayer);
        if (totalGamesPlayed === 0 && registeredNumbers.size === 0 && typeof cardStates !== 'undefined' && cardStates.size === 0) {
             isInPreGameMode = true;
             preGameActiveRange = '1-100';
             enterPreGameRegistrationView();
        } else {
             isInPreGameMode = false;
             setBoardLayout('standard');
             if (calledNumbers.size > 0) {
                updateBoardHighlights();
             }
        }
        updateSettingsUI();
        console.log("Bingo Game Initialized.");
    });
  </script>
</body>
</html>
