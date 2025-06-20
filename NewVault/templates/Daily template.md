---
creation date: <% tp.file.creation_date() %>
modif date: <% tp.file.last_modified_date("Do MMM, YYYY") %>
modif time: <% tp.file.last_modified_date("HH:mm") %>
---
<%* // Set filename to today's date 
await tp.file.move("Daily Notes/" + tp.date.now("Do MMM, Y"));

// Get yesterday's date for achievements
const yesterday = tp.date.now("Do MMM, Y", -1);

// Function to get previous day's achievements 
async function getPreviousAchievements() { 
	const yesterdayFile = tp.file.find_tfile(yesterday); 
	if (yesterdayFile) { 
		const content = await app.vault.read(yesterdayFile); // Extract completed tasks (lines with [x]) 
		const completedTasks = content.split('\n').filter(
			line => line.includes('- [x]')
		).map(
			line => line.replace('- [x]', '✅').trim()
		) .join('\n');
	
	
	// Extract achievements section if it exists
	const achievementMatch = content.match(/## Achievements([\s\S]*?)(?=##|$)/);
	const achievements = achievementMatch ? achievementMatch[1].trim() : '';
	
	if (completedTasks || achievements) {
		return `${completedTasks}\n${achievements}`.trim();
	}
}
return "No achievements found from yesterday";
}

// Function to get recurring tasks 
function getRecurringTasks() { 
return `- [ ] Check emails
- [ ]  Review calendar
- [ ]  Daily standup
- [ ]  End of day review`; 
} %>
# <% tp.date.now("dddd, MMMM Do, YYYY") %>

## Yesterday's Wins 🏆

<%* tR += await getPreviousAchievements(); %>

## Today's Focus 🎯

## Tasks ✅

<% getRecurringTasks() %>
## 📝 Notes 

## Meetings 🤝

## Achievements 🌟

_Add completed tasks and wins here_

---

_Created: <% tp.date.now("YYYY-MM-DD HH:mm") %>