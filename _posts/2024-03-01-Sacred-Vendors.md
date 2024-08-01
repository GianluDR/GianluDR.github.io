---
layout: post
title: "Sacred Vendors"
date: 2024-03-01
categories: [StudioProject,GroupProject]
tags: [C++,Unreal,Blueprints]
image:
  path: /assets/SacredVendors.png
  lqip: data:image/webp;base64,UklGRpoAAABXRUJQVlA4WAoAAAAQAAAADwAABwAAQUxQSDIAAAARL0AmbZurmr57yyIiqE8oiG0bejIYEQTgqiDA9vqnsUSI6H+oAERp2HZ65qP/VIAWAFZQOCBCAAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
  alt: Splash art.
---

## About
Sacred Vendors is an horror stealth game freely inspired by the case of the sale of children in Spain between 1943 and 1987.

## Project info
**👤 Role:**  Lead programmer  
**👥 Team size:**  10  
**⏱︎Time frame:**  4 months, but not ended  
**⚒︎ Engine:**  Unreal Engine 5(C++)  

Players live an anxious experience by impersonating a 8 y/o child with no memories who finds himself in a strange catholic environment chased by nuns, doctors and prelates. His mission is to find a way out and discover who he is and what is happening there. 
The gameplay is based on stealth and environmental interactions mechanics.

### Enemy AI
I had previously created AIs for my previous project, but they were very basic. This time, I had to develop a proper audio and visual perception system. The enemies have their own Behavior Trees, and based on the stimuli they receive, they decide whether to follow their regular path, investigate, or directly chase the player.

```
void ANPC_AIController::SetupPerceptionSystem()
{
	// Sight configuration
	SightConfig = CreateDefaultSubobject<UAISenseConfig_Sight>(TEXT("Sight Config"));
	if (SightConfig)
	{
		SetPerceptionComponent(*CreateDefaultSubobject <UAIPerceptionComponent>(
			TEXT("Perception Component")));
		SightConfig->DetectionByAffiliation.bDetectEnemies = true;
		SightConfig->DetectionByAffiliation.bDetectFriendlies = true;
		SightConfig->DetectionByAffiliation.bDetectNeutrals = true;
        SightConfig->SightRadius = npc->SightRadius;
        SightConfig->LoseSightRadius = npc->LoseSightRadius;
        SightConfig->PeripheralVisionAngleDegrees = npc->PeripheralVisionAngleDegrees;
        SightConfig->SetMaxAge(npc->MaxAgeSight);
        SightConfig->AutoSuccessRangeFromLastSeenLocation = npc->AutoSuccessRangeFromLastSeenLocation;
        PerceptionComponent->ConfigureSense(*SightConfig);


		GetPerceptionComponent()->SetDominantSense(*SightConfig->GetSenseImplementation());
		GetPerceptionComponent()->OnTargetPerceptionUpdated.AddDynamic(this, &ANPC_AIController::OnTargetDetection);
		GetPerceptionComponent()->ConfigureSense(*SightConfig);
	}

	// Sound configuration
	SoundConfig = CreateDefaultSubobject<UAISenseConfig_Hearing>(TEXT("Sound Config"));
	if (SoundConfig)
	{
		SoundConfig->HearingRange = npc->HearingRange;
        SoundConfig->SetMaxAge(npc->MaxAgeSound);
        PerceptionComponent->ConfigureSense(*SoundConfig);
		SoundConfig->DetectionByAffiliation.bDetectEnemies = true;
		SoundConfig->DetectionByAffiliation.bDetectFriendlies = true;
		SoundConfig->DetectionByAffiliation.bDetectNeutrals = true;

		GetPerceptionComponent()->OnPerceptionUpdated.AddDynamic(this, &ANPC_AIController::OnSuspectDetected);
		GetPerceptionComponent()->ConfigureSense(*SoundConfig);
	}
}
```

### Fear system
The player must manage an internal fear system that ranges from 0 to 100. Depending on the player's fear level, they must deal with hallucinations and a more clumsy character, which can cause more noise than usual and potentially attract nearby enemies.

### Sounds configuration
I created a class that manages various sound interactions to avoid duplicated code. Any actor or other entity that wants to play sounds only needs an instance of this class.

## What i learned
I worked differently from usual, using Trello and using a Gantt chart. There was a clear division of roles and departments. Thanks to my role as Lead, I had many interactions and had to make various design and programming decisions due to time constraints and efficiency. Having to make these decisions can be quite stressful, but this experience helped me make better decisions more calmly. It was also my first experience with Unreal Engine; initially, I wasn't the lead, but I got so involved that I improved and eventually attained that position.

## More about...
Further insights can be asked in private, this game is planned to be released so nothing is public.
