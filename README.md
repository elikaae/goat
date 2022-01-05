async function getName() {
    const response = await fetch('https://api.blooket.com/api/users/verify-token', {
        method: "GET",
        headers: {
            "accept": "application/json, text/plain, */*",
            "accept-language": "en-US,en;q=0.9,ru;q=0.8",
        },
        credentials: "include"
    });
    const data = await response.json();

    return data.name;
};

async function addCurrencies() {
    const tokens = Number(prompt('How many tokens do you want to add to your account BOZO? (made by eli)'));

    if (tokens > 500) {
        alert('add as much you want!');
    };

    const response = await fetch('https://api.blooket.com/api/users/add-rewards', {
        method: "PUT",
        headers: {
            "referer": "https://www.blooket.com/",
            "content-type": "application/json",
        },
        credentials: "include",
        body: JSON.stringify({
            addedTokens: tokens,
            addedXp: 300,
            name: await getName()
        })
    });

    if (response.status == 200) {
        alert(`${tokens} tokens and 1,000 XP added to your account! IF YOU GET BANNED THAT IS ON YOU!`);
    } else {
        alert('An error occured.');
    };

};

addCurrencies();
