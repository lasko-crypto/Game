<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Randomized Interactive Story</title>
    <style>
        body { font-family: Arial, sans-serif; text-align: center; background: #f7f7f7; margin-top: 50px; }
        .story-container { background: white; border-radius: 10px; padding: 20px; box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1); }
        button { padding: 15px 30px; margin: 10px; font-size: 18px; cursor: pointer; border-radius: 5px; border: none; background: #3498db; color: white; }
        button:hover { background: #2980b9; }
        .choices { display: flex; justify-content: center; flex-direction: column; }
        .choice { margin: 5px 0; }
    </style>
</head>
<body>

    <h1>Randomized Interactive Story: The Mystery Adventure</h1>
    <div class="story-container">
        <p id="storyText">Loading story...</p>
        <div class="choices">
            <!-- Choices will be dynamically added here -->
        </div>
    </div>

    <script>
        const storyParts = {
            "startAdventure": {
                text: "You wake up in a mysterious place. What will you do next?",
                choices: [
                    { text: "Explore the room", action: "exploreRoom" },
                    { text: "Stay still and listen", action: "stayQuiet" }
                ]
            },
            "exploreRoom": {
                text: "You explore the room and find an old map on the floor. It seems to lead somewhere. What do you do next?",
                choices: [
                    { text: "Follow the map", action: "followMap" },
                    { text: "Ignore it and look for an exit", action: "searchExit" }
                ]
            },
            "stayQuiet": {
                text: "You stay quiet and hear footsteps approaching. Someone opens the door and looks at you. What do you do?",
                choices: [
                    { text: "Speak to the person", action: "speakPerson" },
                    { text: "Stay silent and hide", action: "hide" }
                ]
            },
            "followMap": {
                text: "You follow the map and discover a hidden door leading to a dark tunnel. Do you enter?",
                choices: [
                    { text: "Yes, go in", action: "enterTunnel" },
                    { text: "No, go back", action: "goBack" }
                ]
            },
            "searchExit": {
                text: "You search for an exit but find yourself in a locked room. The walls are closing in! What do you do?",
                choices: [
                    { text: "Try to break the door", action: "breakDoor" },
                    { text: "Wait and hope someone finds you", action: "waitForHelp" }
                ]
            },
            "speakPerson": {
                text: "You speak to the person and they reveal they’ve been waiting for you. It seems like you’ve been chosen. You follow them to the next room.",
                choices: [
                    { text: "Continue following them", action: "followThem" },
                    { text: "Run away", action: "runAway" }
                ]
            },
            "hide": {
                text: "You hide and stay still. The person leaves, and you find an open window to escape.",
                choices: [
                    { text: "Escape through the window", action: "escapeWindow" },
                    { text: "Wait and see if it's safe", action: "waitSafe" }
                ]
            },
            "enterTunnel": {
                text: "You enter the tunnel, but it seems to go on forever. After a while, you hear strange noises from behind. What will you do?",
                choices: [
                    { text: "Keep walking", action: "keepWalking" },
                    { text: "Turn around and face the noise", action: "turnAround" }
                ]
            },
            "goBack": {
                text: "You decide to go back, but the room has changed, and it seems like there's no way out now. You're trapped!",
                choices: [
                    { text: "Look for another exit", action: "lookForExit" },
                    { text: "Yell for help", action: "yellForHelp" }
                ]
            }
        };

        // Randomly pick a starting point for each visit
        const startingPoints = ["startAdventure", "exploreRoom", "stayQuiet"];
        const randomStart = startingPoints[Math.floor(Math.random() * startingPoints.length)];

        function nextPart(part) {
            const partData = storyParts[part];
            document.getElementById("storyText").textContent = partData.text;
            const choicesContainer = document.querySelector(".choices");
            choicesContainer.innerHTML = ''; // Clear previous choices

            partData.choices.forEach(choice => {
                const button = document.createElement("button");
                button.textContent = choice.text;
                button.onclick = () => nextPart(choice.action);
                choicesContainer.appendChild(button);
            });
        }

        // Initialize story with a randomized start
        window.onload = () => nextPart(randomStart);
    </script>

</body>
</html> 

