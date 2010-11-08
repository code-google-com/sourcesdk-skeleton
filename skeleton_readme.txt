SDK SKELETON: A BARE-MINIMUM SOURCE ENGINE GAME
Version 1, 2010-11-8
http://developer.valvesoftware.com/wiki/SDK_Skeleton

This package should be extracted to a folder already containing the SDK's Orange Box source tree (it won't overwrite anything). Open one of the .sln files with Visual Studio to get started. The player entity is configured for multiplayer but will work fine in singleplayer.

The compiled DLLs will appear in in \game\sdk_skeleton. Edit the projects' Custom Build Steps to redirect them to your mod's \bin folder. You will also need to configure debugging.

---

There are at the time of writing errors in Valve's CPP files that you must fix manually:

* http://developer.valvesoftware.com/wiki/Compiling_under_VS2005 (2005 ONLY; the "LNK2019 errors" fix has already been applied)
* http://developer.valvesoftware.com/wiki/Compiling_under_VS2008#Fix_debug_compilation (2008/2010 ONLY)
* http://developer.valvesoftware.com/wiki/Client_missing_DT_class_CWaterBullet

---

MULTIPLAYER

Also included are CBaseNetworkedPlayer, CBaseNetworkedRagdoll and CNetworkedPlayerMovement. These apply Valve's most current multiplayer player techniques to CBasePlayer and CRagdoll, without any extra cruft.

They are not included in the projects by default. If you choose to use them CBaseNetworkedPlayer will need to be implmented by linking it to the "player" classname. Remember to update bots too, if you're using them.

Jumping will not work properly until you edit the PLAYERANIMEVENT_JUMP case in CMultiplayerAnimState::DoAnimationEvent(). Replace RestartMainSequence() with RestartGesture( GESTURE_SLOT_JUMP, ACT_MP_JUMP ). Depending on how you models are animated you may also want to edit CMultiPlayerAnimState::HandleJumping(), particularly where it sets the idealActivity to "jump".

For more help:

* http://developer.valvesoftware.com/wiki/m_PlayerAnimState
* http://developer.valvesoftware.com/wiki/acttable_t

---

The SDK Skeleton was created for the Source SDK and Visual C++ Express 2005/2008/2010 by Tom Edwards (contact@steamreview.org). It is distributed under the terms of the Apache License 2.0 <http://www.apache.org/licenses/LICENSE-2.0.html>.