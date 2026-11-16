# NECOC YAOTL

## Project Origins and Resource Provenance

**Necoc Yaotl was developed from scratch during the 2026 Epic AI MegaJam.** No previous version of the game existed.

**The only pre-authored third-party creative libraries incorporated were Quaternius animations and WeLoveIndies sounds; both were selected and integrated for this game during the jam.** We did not use other third-party model, animation, sound, or art packs. The remaining game-specific content was created or generated during the MegaJam using the tools and AI agents described in this journal.

The sample characters and animations included with Unreal Engine were used temporarily for testing during development; they were not taken from a previously developed game.

---

A dark fantasy, soulslike action game inspired by Mexica civilization.

An ancient sanctuary has been desecrated. Foreign invaders have taken something that should never have left its resting place.

A warrior who once renounced violence is summoned by Tezcatlipoca, an enigmatic deity known as Necoc Yaotl, “The Enemy on Both Sides.”

To confront the invaders, he must take up his weapon once more.

The concept asks what might have happened if we had been ready to repel the invaders...

---

## Development Journal

> **Who made this.** The **director of Yaxché Industries** defines the artistic and narrative vision, goals, priorities, architectural decisions, artistic work, gameplay testing, and visual approval. **ChatGPT (OpenAI)** supported technical planning, analysis of alternatives, conceptual research, proposal and diagnostic reviews, and coordination of instructions among agents. **DeepSeek V4.1 Flash through OpenCode** served as the implementation agent: C++ code, Blueprints, scripts, automation, integration of systems and assets, diagnostics, compilation, static checks, and reporting. **Grok (xAI)** was an earlier collaborator in combat research and architecture, with contributions recorded in Milestone 3 but no involvement in subsequent stages. These attributions come from the director.

### Milestone 1 — Project Foundation

**Goal:** establish the game's foundation in Unreal Engine 5.8 using C++.

**Development:** the `NecocYaotl` project was created and placed in a version-controlled repository, allowing us to work without fear of losing progress and roll back when necessary. We also prepared the repository for game assets—models, maps, sounds—without allowing generated or unnecessary files to make it balloon in size.

DeepSeek V4.1 Flash, used through OpenCode, helped with the initial project and repository setup: Git tools, asset handling, and organizing the first files and documentation. ChatGPT assisted with planning this foundation and coordinating the first tasks, providing technical and organizational analysis.

**Problems and decisions:** the first choice was deciding what deserved preservation. We kept source code, configuration, and game content; we excluded files generated automatically by the engine and editor because they differ between machines and do not tell the project's story. We also decided to write the development diary in Spanish and Git commit messages in English to keep the history orderly.

**Recorded checkpoint:** the repository's first commit was `cef1cae`.

**Result:** a project ready for development, with clean version history and an empty content foundation awaiting its first map.

---

### Milestone 2 — First Playable Foundation

**Goal:** establish a first playable foundation on which to develop Necoc Yaotl's mechanics.

**Development:** we integrated Manny using standard Unreal Engine 5.8 resources and animations. We configured movement, camera, and jumping, while retaining additional animations for possible future use.

We created `L_Test`, a simple map for testing the character.

This technical integration—Manny, locomotion, controls, Blueprints, and preparing `L_Test`—was performed with DeepSeek V4.1 Flash through OpenCode, working alongside the director. ChatGPT helped plan the foundation and discuss technical decisions before implementation.

**Problems and decisions:** we chose to begin with existing engine resources and validate movement before developing custom systems.

**Recorded results:** movement was manually validated in PIE; commit `1ae2e6a` added the Manny base character, input configuration, and `L_Test` map. Screenshots were still pending at this stage.

**Result:** Manny could run, jump, fall, and land correctly in our test map.

---

### Milestone 3 — Research and Architectural Design of the Combat System

**Goal:** research and define an original, modular, and scalable architecture for Necoc Yaotl's combat.

**Development:** combat is at the heart of the game, so before programming the first strike we asked Grok, an early collaborator in this phase, to research genre references and propose an original architecture. This led to defining the main combat systems—including Rally—the responsibilities of each, and how they should communicate. The design was gathered into an architectural proposal that served as a blueprint for implementation.

ChatGPT analyzed and reviewed the proposal, compared alternatives, and helped organize responsibilities before adoption. The director made the final decisions about what to retain and what to remove.

**Problems and decisions:** the temptation was to begin with the first attack animation and solve everything else as we went. We chose the opposite. In a soulslike, combat supports the entire experience; rebuilding its foundations mid-project is much more expensive than thinking them through early. We therefore defined the architecture first—which systems existed, what each decided, and what was outside its responsibility—and postponed implementation. At this historical stage, none of the proposals had yet been implemented.

**Result:** an initial architecture ready to guide combat development; implementation remained pending at this milestone.

---

### Milestone 4 — Day 2 | Combat Starts to Feel Real

**After 44 hours and 13 minutes of the MegaJam, Necoc Yaotl reached its first playable combat foundation.**

**Goal:** move beyond isolated systems and make combat playable from beginning to end against an enemy.

**Development:** the pieces began to come together. We could move, attack, and chain combos; dodge and lock onto enemies; manage stamina and regain health through Rally; block, parry, and retaliate with a counterattack. An enemy could pursue us, telegraph attacks, take damage, lose poise, and die. We also began to give hits a sense of weight through reactions, stagger, and an initial feedback system.

This progress was recorded in commit `5c9a08b` (`feat(combat): establish playable rally-first combat core`).

DeepSeek V4.1 Flash through OpenCode implemented the systems. ChatGPT supported analysis, planning, and troubleshooting. The director decided the scope of this first combat implementation—what was included and what would remain pending.

> For the first time, Necoc Yaotl let us begin to test and feel its combat. We were no longer working exclusively with isolated systems: we could face an enemy, experiment with attack rhythm, appreciate the importance of defense, and start discovering what worked and what needed improvement.

**Problems and decisions:** the experience was still far from final, and this was precisely when a crucial stage began: evaluating the feel of combat through real tests. To avoid confusing progress with proven results, we separated confirmed functionality from remaining work:

- **Implemented and tested in PIE:** movement, attacks, combos, dodge, lock-on, stamina, Rally, block, parry and counterattack, a fully functional enemy, and damage reactions.
- **Compiled and statically verified, pending gameplay testing:** hit feedback (very brief pauses, camera shake, flashes of light, and hooks reserved for audio).
- **Provisional:** animations still came from Manny, the weapon was a test stick, and audio had no sounds assigned yet.
- **Outside this milestone:** player hit reactions, hyperarmor, equipment, and projectiles.

The first gameplay discovery came quickly: **the enemy resumed its offense too soon after being parried**. We recorded this for adjustment during the next polishing pass.

**Recorded checks:** commit `5c9a08b`; Unreal Engine 5.8 compilation without warnings; in-editor gameplay testing performed by the director.

**Result:** a stable first one-on-one combat system with attacks, defense, reactions, and death working together.

**Next steps at the time:** integrate **WeLoveIndies audio** to establish a sonic identity for combat, and replace the temporary stick with an **original weapon designed by Yaxché Industries**. Afterward, continue comprehensive validation and polish.

---

### Milestone 5 — Graybox Environment and First Enemy AI

**Goal:** build Necoc Yaotl's first playable dungeon as a laboratory for combat and navigation, and develop the first enemy AI capable of detecting, pursuing, attacking, losing, and reacquiring the player.

**Development — environment:** `L_RitualDungeon_Graybox` was created with graybox geometry and materials. It was not a completed art level, but a working space to test combat, routes, and navigation. It included:

- Initial ritual chamber.
- Corridors and intersections.
- Secondary routes.
- Central plaza.
- Side rooms.
- Provisional boss room, with neither a boss nor a victory condition implemented yet.
- Ten placed enemies.
- Graybox materials and geometry.
- NavMesh for pursuit and returning home.

The environment allowed us to reproduce encounters, measure distances, test routes, and observe how AI reacted to obstacles, walls, height differences, and player positioning.

**Development — enemy AI:** AI was built on the existing `AEnemy` and its finite state machine, without Behavior Trees or AI Perception. We reused `AAIController`, NavMesh, Path Following, and RVO. Development proceeded incrementally:

- **AI-1 — Navigation:** connected `AEnemy` to `AAIController` and NavMesh, with pursuit through Path Following and RVO avoidance.
- **AI-1.1 — Detection and locomotion:** corrected acceleration so Walk/Run animations responded to movement; dual detection through 360-degree proximity and forward-facing vision, both with line-of-sight checks.
- **AI-1.2 — Recovery:** corrected arrival at Home, added navigation retries with cooldown, recovery after `PATH_FAIL`, destination projection, and decision logs (`RETURN_COMPLETE`, `PATH_RETRY`, `TARGET_UNREACHABLE`, and others).
- **AI-1.3 — Three-dimensional perception:** 300 cm proximity; 120-degree horizontal and ±30-degree vertical FOV; multipoint visibility to head, chest, and pelvis; continuous tracking while LOS remained to at least one point; leash with 1.5-second grace period, maximum 300 cm margin, and 200 cm hysteresis.
- **AI-1.4 — Visual tools:** restored four debug layers—awareness, volumes, raycasts, and navigation—with a 3D vision cone, perception and attack rays, Home/leash/last-position/path markers, observation/tracking/search/return indicators, and automatic focus with visualization controls.

Debugging was not decoration: it was a reusable way to understand what an enemy saw, decided, and why it abandoned or recovered a target. Automatic focus changed the level of detail without hiding information about other enemies.

**Actual state of development:**

- **Implemented:** graybox level; NavMesh; AI navigation, detection, pursuit, attack, target loss, and return; multipoint perception and leash; four debug layers; existing combat system and Macuahuitl.
- **Validated:** successful compilations of AI-1.2, AI-1.3, and AI-1.4 without errors or warnings; PIE tests recorded during AI-1/AI-1.1/AI-1.2 for navigation, proximity, pursuit, Home return, and re-detection. Complete visual validation of AI-1.3 and AI-1.4 remained with the director.
- **Pending:** full visual validation of AI-1.4; group-combat refinement; critical attack after Stance Break; jumping attack; correction of enemy death pose; hitbox/hurtbox refinement; boss and victory condition.

**Problems and decisions:** AI development followed a clear principle: instrument, reproduce, and understand first; correct second. When investigating abandoned pursuit, we distinguished genuine LOS loss, leash, `PATH_FAIL`, and player invalidation, rather than blaming a low platform without evidence. This discipline prevented a visual hypothesis from becoming the wrong correction.

We also decided that visual validation belonged exclusively to the director. An agent could compile, review code, inspect properties, and provide static evidence, but could not replace gameplay experience. Debug tools were designed to make the director's validation quick and understandable.

DeepSeek V4.1 Flash through OpenCode implemented the level, navigation, perception, return behavior, and debug layers; ChatGPT supported planning and diagnosis. The director defined the desired AI behavior and performed in-game validation.

**Recorded checks:** the graybox map, successful AI-1.2/AI-1.3/AI-1.4 compilations, and PIE tests for AI-1/AI-1.1/AI-1.2. Commit `0d5b978` captured combat audio, the Macuahuitl, parry recovery, and graybox progress. This milestone was documented before its own commit.

**Result:** a first test dungeon and an enemy AI able to detect, pursue, attack, lose, search for, and return from a target, with tools for understanding and refining that behavior. It was neither a finished level nor a completed boss encounter, but a playable foundation on which to build.

**Next steps at the time:** visually validate AI-1.4, refine group combat and Stance Break criticals, resolve jumping attacks and enemy death poses, adjust hitboxes/hurtboxes, and move toward a boss and win condition.

---
### Milestone 6 — Animation, Rigging, and Retargeting (Hell)

> **Evidence note.** This milestone distinguishes three types of statements: **VERIFIED** (supported by an inspected file, measurement, log, code, or commit), **REPORTED BY THE DIRECTOR** (a decision or experience described during development without a located formal report), and **PENDING** (unfinished work or an unvalidated result). A successful import is not an approved animation. A generated file is not an integrated character.

**Goal:** document what had so far been the most difficult stage in Necoc Yaotl's development: our first serious confrontation with animation, rigging, skinning, and retargeting. This is not the story of a clean success but a series of investigations, mistakes, experiments, partial fixes, scope decisions, and lessons that allowed development to continue.

**Overall outcome:** Necoc's custom rig advanced into a documented, controllable foundation; Quaternius retargeting did not produce an approved animation; the game remained functional by reusing native Unreal animations; and combat, stealth, and critical attacks progressed using that provisional foundation. Animation-related technical debt remained open.

#### 1. The initial problem: we wanted a warrior, not a mannequin

The original ambition was not simply to have a good-looking 3D model. We wanted a dark fantasy warrior inspired by Mexica culture, armed with a Macuahuitl, capable of moving with weight, attacking deliberately, blocking, parrying, dodging, counterattacking, and eventually performing critical blows and finishers. That warrior had to feel like a character, not a static figure sliding through the level.

At first, the problem appeared smaller than it really was. We had experience with programming, software architecture, data, and systems. We knew how to decompose a problem, define contracts, and build tools. What we lacked was specific experience with the artistic pipeline of an animated character. That distinction mattered.

A playable character is not just a mesh. It is a chain of transformations:

1. **Geometry:** a mesh with proportions, silhouette, and materials.
2. **Topology:** a distribution of faces and edges suitable for deformation.
3. **Skeleton:** a bone hierarchy with a coherent rest pose.
4. **Skinning:** weights assigning vertices to the correct bones.
5. **Controls:** an animation layer allowing the skeleton to be manipulated without breaking it.
6. **Actions:** clips with duration, frames, curves, and movement conventions.
7. **Transfer:** retargeting or adapting animation between different skeletons.
8. **Animation Blueprints:** logic that determines which animation plays and how animations blend.
9. **Combat and hit detection:** the relationship between visible motion, weapons, attack windows, and actual damage.

Every stage has inputs, outputs, dependencies, and acceptance criteria. We did not know all of them at the beginning. We underestimated integration costs because we looked at the mesh and saw a character; the real cost lay in the entire chain. This lack of experience does not erase our software-engineering background, but it shows that background alone was insufficient. Knowing how to build systems does not automatically teach you how to build an animated character.

#### 2. First stage: character generation and rigging problems

Our first approach was to generate our own character and bring it into Blender. The director reported experimenting with Tripo/TripoSG and a custom-character workflow. The character-generation steps are **REPORTED BY THE DIRECTOR**, while the resulting Blender rig and mesh properties were inspected directly. No unconfirmed generation metrics are presented as verified.

The working model had a `ProtaCuerpoBase` skeleton with **109 bones**, a `ProtaCuerpoBaseMesh` mesh with **79 vertex groups** and an Armature modifier, and **zero actions**. The `Macuahuitl`, `ProtaCasco`, `ProtaCollar`, and `ProtaFaldon` parts existed as separate meshes without vertex groups or armature modifiers in that version. In other words, there was geometry and a skeleton, but not yet a complete character ready to animate as a unit.

We observed several problems:

- **Hand topology and deformation.** Fingers are among the hardest parts of a character: many bones, short distances between joints, and a silhouette extremely sensitive to weight distribution. A generated mesh can look right at rest and deform badly when the hand closes.
- **Incorrect finger weights.** Having finger bones does not guarantee the proper vertices are influenced by them. Bad weights make fingers sink, stretch, or drag palm geometry.
- **Skeleton compatibility.** The generated skeleton was not Manny's. Hierarchy, names, rest pose, and proportions did not automatically match.
- **Different proportions.** A character with different proportions from Unreal's mannequin cannot inherit an animation without adaptation. The same bone rotation can look different when bone length or orientation changes.
- **Joints failing to follow the expected animation.** Motion could exist in the source clip yet fail to move the leg, arm, or foot as expected. The problem might lie in the clip, rig, weights, or import.
- **Difficulty connecting the custom character to Manny's locomotion.** Manny was useful as a provisional base, but not the final protagonist. Reusing his locomotion with a different mesh required adaptation that had not been solved.

An uncomfortable early lesson emerged: **generating a mesh does not solve the problem of making it animatable**. Generation can produce a shape; rigging and skinning produce a body that can move. They are distinct problems.

Two characters also need to be distinguished:

- **The custom Blender character:** Necoc's artistic character project, with its own skeleton and rigging problems.
- **Manny, Unreal's temporary mannequin:** a provisional playable protagonist used to implement and test locomotion, combat, and mechanics while the definitive character was still being developed.

Confusing these two leads to false conclusions. Manny moving does not mean the Mexica warrior has been integrated. A skeleton in Blender does not mean that character is playable in Unreal.

#### 3. Rokoko: a promising but insufficient solution

Our next investigation involved Rokoko. The idea was appealing: use motion capture or motion resources to achieve more natural animation than we could create from scratch. The experiment produced a heavy-attack FBX animation.

**Verified technical properties:** importing that FBX into Blender yielded an **80-bone armature**, with a `root` bone and a main action spanning **frames 1–131**. The file existed, was importable, and contained motion. These were technical facts.

What we could not claim was that the animation had passed visual approval. Problems diagnosed during testing included:

- **Y-up/Z-up axis conversion.** Motion data may be correct in its originating tool and arrive rotated or oriented unexpectedly.
- **Orientation correction.** Adjusting one axis does not necessarily solve the whole problem; a clip may align on one axis but not another.
- **Height offsets.** The character can float above or sink into the ground.
- **Foot penetration.** A clip that looks right in a viewer may push feet through the floor when applied to a different skeleton or scale.
- **Small rotational differences.** Minor accumulated errors in hips, knees, or ankles can radically change the movement's appearance.
- **The need for baking and visual review.** Importing is not the same as baking and validating; baking can introduce or expose problems.
- **Import success versus usable animation.** A file opening without errors does not mean the character walks, attacks, or lands correctly.

The **80-bone** count matched the reported hierarchy compatibility with the custom skeleton. But that number must not become a promise. Eighty animatable bones do not guarantee that rest pose, proportions, pivots, weights, and orientation will produce an acceptable result. Numerical compatibility is necessary, not sufficient.

Our decision was not to declare Rokoko technically impossible or pretend it was never used. We decided **not to make it an essential production dependency**. It did not solve the complete problem fast enough and introduced another configuration chain we did not yet control.

Diagnosing each failure was costly. Incorrect motion could originate in:

1. the motion file;
2. the original rig;
3. coordinate conversion;
4. retargeting;
5. skinning;
6. the target skeleton;
7. scale or pivots;
8. Unreal's import behavior.

Investigating each possibility without adequate observability consumes time and creates false positives. That experience directly shaped our later method: instrument before correcting.

#### 4. iClone 8 and the temptation to add more tools

During our exploration of animation options, the director reported installing and activating **Reallusion iClone 8 PERSONAL**. No animation originating from iClone was confirmed as integrated into Necoc Yaotl. Therefore:

- **REPORTED:** iClone 8 PERSONAL was installed and activated as an animation alternative.
- **NOT PRESENTED AS INTEGRATED:** no iClone animation is counted among the game's completed assets.
- **PENDING / NOT CLAIMED:** its full capabilities were not exhaustively evaluated.

Other AI-assisted animation alternatives were also explored, but no completed game assets are attributed to them without a confirmed result. An installed tool is not a produced animation; an exploratory test is not a production pipeline.

We decided to stop accumulating tools. Each new tool meant another format, configuration, axis convention, export step, and failure mode. Under time pressure, adding steps can look like progress while actually increasing uncertainty. The useful question changed from “What other tool could we try?” to “Which part of this pipeline can we control and verify using what we already have?”

#### 5. Necoc's custom rig: beginning to understand the skeleton

The central custom rig was a work in progress, built on Tripo's original skeleton. It was one of the clearest signs that we were beginning to understand character structure, but it was **not a finished rig**.

**Verified state of the most recent inspected rig:**

- `ProtaCuerpoBase` armature with **185 bones**.
- **109 original** Tripo skeleton bones.
- **70 `CTRL_`-prefixed bones**.
- **6 auxiliary `MCH_` bones**.
- **70 constraints** in total: **64 COPY_TRANSFORMS**, **2 IK**, and **4 CHILD_OF**.
- **Zero actions** stored in the controls version.
- `ProtaCuerpoBaseMesh` with **79 vertex groups** and an Armature modifier.
- Custom widget meshes: `WGT_Ctrl_Body`, `WGT_Ctrl_Finger`, `WGT_Ctrl_Limb`, and `WGT_Ctrl_Root`.

**Verified evolution:**

- Initial version: **109 bones**, no controls, constraints, or actions.
- Animation-experiment version: retained the **109-bone** base, contained **97 actions**, a test armature with **79 COPY_ROTATION constraints**, a `root` armature with **167 bones**, and a Manny mesh. This showed interoperability experiments with Manny, not completed integration.
- Controls version: **185 bones**, **70 CTRL**, **6 MCH**, **70 constraints**, and **zero actions**.

Earlier stages of the rig were described as **175 bones / 66 controls / 64 constraints**, then approximately **180 bones / 67 controls / 67 constraints**. These are **HISTORICAL COUNTS REPORTED BY THE DIRECTOR**, not the final state. The inspected version was **185/70/70**. The difference means the rig continued to evolve; older numbers should not be presented as the final count.

The control design aimed to build a visible, understandable layer on top of the original skeleton:

- **CTRL_Master** and **CTRL_COG** as global controls.
- **CTRL_Pelvis**, spine chain, **CTRL_Chest**, neck, and head.
- Clavicles, arms, and hands.
- Finger controls on both hands.
- **CTRL_Thigh_L/R**, **CTRL_Calf_L/R**, and **CTRL_Foot_L/R**.
- **CTRL_IK_Foot_L/R**, **CTRL_Ball_L/R**, and **CTRL_Pole_Knee_L/R**.
- `MCH_IK_*` bones for leg mechanics.

The hierarchy and constraints had a specific goal: controls should respond directly in **Pose Mode**, without selecting the correct deforming bone for every test. We also had to preserve the **Rest Pose** and isolate changes rather than destroy the original rig.

The problems arose precisely there:

- Moving one control could unexpectedly deform a different body part.
- A badly oriented constraint could misalign the visible control and deforming bone.
- Left-leg IK needed careful chain, pole, and foot configuration.
- Changing the rest pose or a control's orientation could affect every clip.
- Isolating a change without damaging the existing hierarchy was harder than adding a new control.

The goal was not to get an animation to play once; it was to build a comprehensible, controllable base for future work. By that measure, the rig progressed: controls, constraints, and mechanical bones existed. But **it was not finished**. “Rigging foundation in progress” was accurate; “final animated character” was not.

#### 6. Skinning: the problem was not always the animation

This was one of the milestone's most important lessons. For a long time, strange movement could be blamed on an animation. Investigation showed that bone weights could be the actual cause.

Our analysis focused on knees, ankles, heels, toes, twist bones, vertex-group distribution, weight transfers, and rotational deformations.

Reported findings included:

- **Excessive `thigh_twist_02` influence** near the calf: the thigh twist dragged geometry that should belong to the lower-leg chain.
- **Incorrect `calf_twist_01` influence** over the heels: if a calf twist controls the heel, its shape collapses during rotation.
- **Weight transfers** producing stretching and loss of volume.
- **Abrupt influence transitions** between bone chains, producing visible pinches, twists, and collapses.

Our **K5 rule**, inspired by functional behavior we had already identified in the elbow, can be summarized as follows:

> The transition from a proximal to a distal chain should be gradual; volume should be preserved; weights should reflect the actual geometry of the joint.

K5 is not a magic button. It is an inspection criterion: examine where each bone's influence begins and ends, how it is distributed around the joint, and what happens when the chain rotates. Applying it to the knees produced an improvement visually approved by the director. That approval is **REPORTED BY THE DIRECTOR**; no screenshot or numeric deformation report independently replaces that judgment.

A failed attempt was also documented:

- An **abrupt weight transfer on the left foot** was attempted.
- The result was unacceptable.
- **Original weights were restored**.
- Additional **ankle and toe corrections were deliberately paused**.

The latest inspected body mesh still had **79 vertex groups**. It did not retain the failed transfer, consistent with the reported restoration but not proof on its own. The important decision was not to leave a dubious fix in place merely because it had taken time to create.

**Documented outcome:** K5 on both knees, visually approved by the director; unsuccessful left-foot transfer reverted; ankles and toes pending. **We do not claim to have fixed the feet or ankles.**

The lesson was clear: **changing animations does not fix defective skinning**. If weights are wrong, even the best clip will deform badly. Before chasing another animation, we must know whether the body can receive it.

#### 7. Quaternius: the second major experiment in reuse

Our second major experiment was reusing existing animations. We investigated Quaternius's **Universal Animation Library** and **Universal Animation Library 2**, alongside `MegaJam_Preview`, Manny, and Quinn.

**Verified properties of the external libraries:**

- UAL1: a **65-bone** armature and **43 actions**.
- UAL2: a **65-bone** armature and **43 actions**.
- UAL1 actions included `Crouch_Idle_Loop`, `Crouch_Fwd_Loop`, `Sword_Idle`, and `Sword_Attack`.
- UAL2 actions included `Sword_Block`, `Sword_Dash`, `Sword_Heavy_Combo`, `Sword_Regular_A`, `Sword_Regular_A_Rec`, `Sword_Regular_B`, `Sword_Regular_B_Rec`, `Sword_Regular_C`, `Sword_Regular_Combo`, and `Hit_Knockback`.
- The libraries were distributed under the **CC0 1.0 Universal / Public Domain Dedication**, with attribution to **@Quaternius**. Their provenance and licensing were checked locally.

The phase record indicates that **14 Quaternius AnimSequences** were imported into Unreal, alongside **two source 65-bone skeletons** and two SkeletalMeshes. The target was `SK_Mannequin`, whose structure was considerably larger. Import was technically possible; visual integration remained unresolved.

The problems included:

- **Hierarchy differences.** A 65-bone skeleton does not have the same structure as `SK_Mannequin`.
- **Different reference poses.** Source and target rest poses do not automatically match.
- **Retargeting challenges.** Transferring rotations between skeletons with different proportions and conventions creates deformations unless configured carefully.
- **Limited MCP access to IK Rig/IK Retargeter.** Editor tools available to the agent did not expose a complete, safe route for creating and configuring retargeting.
- **Unreal Python and alternative imports.** We investigated Unreal's Python interpreter, IK Rig/IK Retargeter creation, and direct imports. The Python plugin was enabled, but the available interface did not support unrestricted execution of the necessary API; console/OS automation was not used as a workaround because of risk and project restrictions.
- **UE 5.8 Auto Retargeting.** We attempted to retarget `Crouch_Idle_Loop` to Manny using Auto Retargeting.

**Visual result of Auto Retargeting: incorrect.** The director observed deformed arms and legs and an incompatible posture. The export was not approved as a final animation. At this stage, no approved retargeted asset existed in the project. This demonstrated that importing and retargeting are separate stages, and that automated output still requires technical and visual validation.

We also examined `MegaJam_Preview`: it did not contain new crouch, backstab, riposte, or execution animations—only template montages and Animation Blueprints, not the final material we sought. This kept us from relying on resources that were not actually present.

We ultimately decided to remove **18 imported Quaternius assets** from the project: **14 AnimSequences, two SkeletalMeshes, and two Skeletons**. Before deletion, we verified that the imported animations had no external referencers, while source skeletons and meshes only referenced each other and their animations within the same import group. The imported folders were emptied and removed. **The original libraries on disk were untouched.**

This was a **scope-control decision**, not a judgment that Quaternius was a poor library. It was useful, but integrating it correctly within the deadline proved too costly. Retaining imported assets with no approved integration path would have added clutter and technical debt.

#### 8. The decision: use what works and do not block the game

Available pre-existing animations did not fully cover our artistic needs or all planned actions. Nevertheless, development had to continue. We decided to reuse native Unreal animations temporarily to preserve working gameplay.

This distinction matters:

> **We did not choose native animations because they were our final artistic solution, but because they were sufficient to implement and verify gameplay mechanics.**

The provisional strategy included:

- **Manny** as a temporary playable character.
- **MM_Attack_03** and other native attack sequences.
- Native enemy hit reactions and death animations.
- Standing locomotion as a provisional visual representation of stealth.
- A visible Macuahuitl whose attack DataAssets still retained test-weapon (`DA_Stick_*`) configuration, as seen during PIE.
- Final crouch, backstab, and riposte animations **pending**.

We did not claim synchronized cinematic executions were implemented. The existing backstab was provisional: it used `MM_Attack_03`, a native rear hit reaction, and a native rear death. That was sufficient to validate mechanics, not to deliver the final staging.

Necoc's custom rig was still a separate technical project. It should not be confused with completed Unreal integration. The Blender character and playable Manny were two paths that had not yet converged.

#### 9. The methodology that allowed us to move forward

The most useful part of this stage was not a particular tool. It was applying a methodology we already knew—data engineering—to an unfamiliar problem.

We did not literally build an animation ETL system or an orchestrator that automatically converted clips. We **applied data-engineering concepts** to an artistic pipeline.

##### A. Production pipeline

`Model → rig → skinning → controls → animation → Unreal → gameplay`.

Each stage was treated as a transformation with inputs, outputs, dependencies, acceptance conditions, and possible failures.

This helped us stop saying “animation does not work” and start asking **where in the chain it broke**.

##### B. Data contracts

In data engineering, systems integrate when their schemas and contracts are compatible. In animation, these contracts include bone names and IDs, hierarchies, Rest Pose, scale units, coordinate axes, pivots, duration and frames, root-motion conventions, and asset references.

A clip can be valid while violating the target skeleton's contract. Matching names are not enough if hierarchy or rest pose differs.

##### C. Data quality and validation

We did not accept a process merely because it ended without errors. We distinguished:

- generated file;
- imported file;
- technically compatible skeleton;
- acceptable deformation;
- playable movement;
- user-validated functionality.

This distinction was crucial. There were moments when a file existed and a process had “finished successfully,” but its visual output was unacceptable. Declaring success at the first step would have been a mistake.

##### D. Observability

Instrumentation helped us understand problems through weight and deformation reports, bone/count comparisons, Unreal logs, AI states, raycasts, and four-layer visual debugging.

**AI-1.4** is the clearest gameplay example: awareness, vision cone, head/chest/pelvis rays, attack rays, navigation, Home, leash, path, and diagnostic text. These were tools to understand why an enemy detected, lost, or reacquired the player, not decorations. We later applied the same idea to stealth and criticals: `StealthMode`, `ProximitySuppressed`, `BackstabEligible`, `CriticalReason`, `CriticalWindow`, and `CriticalConsumed`.

##### E. Reproducibility and rollback

Development progressed through checkpoints, Git, preservation of original files, scoped changes, restoration of original weights after failed fixes, and avoiding changes to systems that had already met their acceptance criteria.

Restoring the left foot's weights was a small but important example: a failed fix did not stay in the project out of pride. We reverted it and documented why.

##### F. Architecture before implementation

Our process was:

`PLAN → review → BUILD → technical validation → director's visual validation → acceptance or correction`.

Architectural proposals and responsibility contracts were more useful than blind iteration. Before changing a system, we defined what it owned, what it did not own, and how success would be checked. This prevented an animation issue from becoming an unnecessary combat refactor.

#### 10. The role of AI and agents

AI agents collaborated on this project. Hiding their role would be dishonest; giving them all the credit would be equally inaccurate.

The director defined objectives, priorities, and acceptance criteria. Agents researched, proposed architectures, inspected files, and executed authorized changes. **DeepSeek V4.1 Flash through OpenCode** contributed code, diagnoses, setup, compilation, and reports. Scope and acceptance decisions belonged to the director. All visual gameplay validation was performed exclusively by the director.

**ChatGPT** contributed throughout by researching alternatives when we were blocked, comparing proposals, and helping rethink our approach. **Grok** had previously contributed combat research and architecture in Milestone 3; it did not continue into later stages.

Our collaboration also had mistakes:

- research that took too long;
- attempts to solve problems outside scope;
- difficulty distinguishing technical progress from visible progress;
- the need to strictly constrain agents' responsibilities.

The organizational solution was to define roles and stop agents spending time on visual tests. Agents could compile, inspect code and properties, and deliver static evidence. They could not replace the experience of playing. The director played, observed, felt, and decided.

#### 11. What we managed to advance thanks to this decision

Choosing not to let animation block the project allowed parallel progress in:

- **Graybox level:** `L_RitualDungeon_Graybox`.
- **First enemy AI:** navigation, perception, and combat.
- **3D navigation and perception:** proximity, FOV, multipoint LOS, leash, and return behavior.
- **AI-1.4 debug:** four layers.
- **Combat:** parry, counter, Poise, Stance Break, and reactions.
- **Provisional stealth using C:** suppressed only the 300 cm proximity check while retaining FOV, LOS, memory, tracking, alerts, and navigation.
- **Unified critical system using R:** priority `ParryRiposte → StanceBreak → Backstab`, with fallback to the previous counter.
- **Backstab damage:** 120 against a 100-HP enemy.
- **Test enemy death:** a rear-facing death animation.

Directly observed PIE logging included:

```text
[STEALTH] ON speed=150 max=150
[CRIT] VICTIM_PREP BP_Enemy_C_0 reason=1 behind=1 state=IDLE
[CRIT] START reason=1 victim=BP_Enemy_C_0 mult=4.0 dmg=120.0 impact=0.45s range=270 seq=MM_Attack_03
[F1] APPLIED final=120.00 applied=100.00 hp=0.00/100.00 rally=0.00 token=1
[F7] ENEMY_DEAD BP_Enemy_C_0
[F7] ENEMY_DEATH_ANIM BP_Enemy_C_0 seq=MM_Death_Back_01 length=1.10s holdPose=1
[CRIT] IMPACT reason=1 victim=BP_Enemy_C_0 incoming=120.0 final=120.0 applied=100.0 blocked=0 parried=0
```

The map also contained `BP_Enemy_StealthTest_1` (internal instance `BP_Enemy_C_0`) at `(250, 0, 92)`, 500 cm from `PlayerStart`, facing away from the spawn, with 100 HP, 100 Poise, and intact AI.

An important distinction:

- **Backstab:** tested in PIE by the director, with hit and death logs. **VERIFIED through the director's log.**
- **ParryRiposte and Stance Break critical:** implemented and compiled, but **complete validation remained pending**.
- **Final animations:** pending; the backstab was still provisional.
- **Custom rig:** progress documented, not complete.

This gameplay test must not be confused with completion of the custom rig.

#### 12. The director's reflection

The hardest part of the project was not writing combat code. It was discovering how much we did not know about building an animated character.

We began with a clear idea of the warrior we wanted and reasonable confidence in our ability to build systems. That confidence was justified, but insufficient. An animated character is not solved with a mesh, skeleton, and clip; it requires understanding a chain of contracts.

We tried to take advantage of existing tools and animations, only to discover that every integration has its own contracts and costs. An imported file is not a moving character. A compatible skeleton is not an acceptable deformation. A playing animation is not necessarily one that feels good.

Our experience in data engineering did not automatically teach us animation. It gave us a method for avoiding blind work. It taught us to ask where the chain broke, which contract was being violated, and what evidence existed before declaring something functional.

When a system failed, we investigated whether the failure lay in geometry, bones, weights, animation, import, or gameplay. That question saved more time than any new tool. It forced us to accept multiple possible causes and to recognize that an apparently visual fix might not be the correct technical fix.

We did not solve everything. We learned to distinguish immediate blockers from problems that could wait. The knees improved; ankles and feet remained pending. Rigging advanced; final integration was incomplete. Quaternius retargeting produced no approved animation, so we removed those imported assets rather than carry unresolved debt into the deadline.

Progress came when we prioritized an observable, verifiable architecture small enough to finish. It was not spectacular progress. It was honest progress: stop attempting to solve everything simultaneously, instrument what we had, preserve what worked, and record what remained.

We called this milestone **Hell** because it captures genuine difficulty, frustration, fast learning, and costly decisions—not because every issue was solved. If this stage demonstrates anything, it is that animation is not a decorative detail added at the end. It is a discipline with its own rules, and anyone who underestimates it pays the price at the worst possible moment.

#### 13. Actual state and technical debt at this milestone

**Achieved or verified:**

- Functional combat architecture involving `FCombatHitResolver`, attributes, defense, Poise, and reactions.
- AI-1.4 and a four-layer visual diagnosis system.
- Graybox dungeon with ten original enemies and one additional test enemy.
- Custom-rig progress: 109 original bones preserved, 70 controls, six mechanical bones, and 70 constraints.
- K5 corrections on both knees, visually approved by the director according to the phase record.
- Provisional C-key stealth with proximity suppression.
- R-key backstab with 4× damage and rear death.
- ParryRiposte and Stance Break critical implemented and compiled.
- Lethal backstab recorded in PIE: 120 damage requested, 100 applied, 100-HP enemy killed.
- Graybox test enemy placed, oriented, and saved.

**Pending:**

- Complete and validate the custom rig.
- Remaining foot and ankle issues.
- Final stealth/crouch animations.
- Retargeting or original production of final animations.
- Synchronized backstab/riposte executions and staging.
- Complete validation of parry and Stance Break criticals.
- Polish enemy deaths and transitions.
- Final integration of the custom character in Unreal.
- Playable ending and delivery packaging.

We do not conceal technical debt or present unfinished experiments as completed features. The project had a playable base and clear direction, but unresolved animation and artistic work.

#### 14. Evidence limits and traceability at this stage

The work was supported by the recorded Git checkpoints, inspected Blender rigs and animation libraries, combat code, AI/debug behavior, PIE logs, and the graybox level. In particular, the inspected rig had 185 bones (109 original, 70 controls, six mechanical) and 70 constraints, while the Rokoko experiment contained 80 bones and frames 1–131. Both Universal Animation Libraries had 65 bones and 43 actions, with locally checked CC0 licensing.

Limits of this evidence:

- Complete formal metrics for Tripo/TripoSG, Rokoko, iClone, and Auto Retargeting were not available; the related experiences were marked **REPORTED BY THE DIRECTOR**.
- Screenshots or videos of the retargeting and skinning tests were not preserved in the repository.
- Historical rig counts (175/66/64 and approximately 180/67/67) were not treated as the final inspected state.
- Visual approval of the knees and rejection of Quaternius retargeting were director decisions, not automated measurements.
- The backstab was supported by logs but was not presented as a final cinematic execution.

This milestone does not pretend that everything succeeded. It records how we worked, what we learned, and what was still pending.

---
### Milestone 7 — The Import Pipeline Stops Being a Bottleneck

**Goal:** turn importing a Tripo model and its textures from a one-off manual task into a repeatable operation that could be executed in the open Unreal Editor.

**Development:** when we reached this milestone, the initial Yaxché import workflow required a JSON descriptor for every object and performed no geometric measurements: it imported and trusted. We improved that workflow during the jam rather than building a competing system. This was development work for Necoc Yaotl, not a claim that an import pipeline had been completed for the game before November 12:

- Read-only geometric inspection of FBX vertices, transforms, polygons, and triangles, allowing dimensional comparisons.
- Profile-based unit handling: the ×100 correction for Tripo FBXs is applied **only** when its signature appears (`tripo_node_*`, `tripo_mat_*`, `UnitScaleFactor=1`, and metric-scale magnitudes). Ambiguous units stop the process before writing.
- Folder discovery: locate the FBX, choose the texture folder, infer names and destination.
- Eleven-point validation against source geometry and data: mesh, triangles, three axes, pivot, LOD, textures, material, connections, assignment, collision, and saving, with `SUCCESS`, `INCOMPLETE`, or `FAILED` status.
- One idempotent `auto` command supporting `import`, `audit`, and `dry-run`: existing assets are audited, not overwritten.

**Problems and decisions:**

- The mesh was never saved: the importer created a StaticMesh and left it in memory. We corrected this with selective saving (`created-only`), never `Save All`.
- `mark_package_dirty()` is unavailable in UE 5.8's Python API, causing material assignment to fail after import. We replaced it with `modify()` and verified saving.
- `StaticMeshEditorSubsystem` is absent in a commandlet, so convex collision was not being generated. We added `EditorStaticMeshLibrary` as a fallback. That API can return `False` despite successfully creating a hull: checking actual `convex_elems` is more reliable than trusting the return value.
- We did not blindly apply ×100: we checked it against the Tezcatlipoca statue already evaluated at an earlier stage **of this jam** (raw height 2.2147 → 221.47 cm) and against FBX geometry.

DeepSeek V4.1 Flash through OpenCode developed and technically verified the importer. ChatGPT analyzed alternatives and reviewed technical decisions. The director approved procedures, acceptance criteria, and visual model validation.

**Result:** `Pilar1` and `Bracero` were imported and validated as one batch.

| Asset | Triangles (source/UE) | X (cm) | Y (cm) | Z (cm) | Maximum deviation |
|---|---|---|---|---|---|
| `SM_Temple_Pillar_01` | 9,427 / 9,427 | 108.5449 | 108.8379 | 299.8535 | 0.000009 cm (0.000003%) |
| `SM_Bracero` | 10,770 / 10,770 | 95.4590 | 94.0918 | 99.9512 | 0.000011 cm (0.000012%) |

All twelve assets (two meshes, two materials, and eight 4096×4096 textures) were saved, with PBR correctly connected (BaseColor and Normal using RGB; Metallic and Roughness using the R channel in `LinearGrayscale`), convex collision present, and no dirty assets remaining. A second run recognized the assets and audited them instead of duplicating them.

**Evidence limitations:**

- Execution was verified in a commandlet using the same script and workflow. Running it directly from the open editor console remained **PENDING DIRECTOR TESTING**, because the available MCP could not inject text into Unreal's console.
- FBXs declared centimeters although the magnitudes were metric; the ×100 interpretation was validated using the statue, not formally documented by the vendor.
- `Pilar1` textures were JPEG files with `.png` extensions; Unreal identified them by file contents. Neither model had an ambient-occlusion map, and none was invented.
- Visual validation in the level belonged to the director; the importer did not place objects in the scene.

**Technical verification:** the importer was checked for unit handling, folder discovery, geometric validation, and repeatable execution. Bounds, triangle counts, dimensions, and material inputs were inspected through MCP checks during development.

---

### Milestone 8 — The Warrior Finally Comes to Life

> **Evidence note.** As in Milestone 6, this section distinguishes **VERIFIED** (inspected files, measurements, code, or logs), **REPORTED BY THE DIRECTOR** (his decisions and experiences), and **PENDING** (unfinished or unvalidated work). Importing a mesh is not the same as having a playable character, and seeing a weapon is not the same as completing combat.

**Goal:** replace Manny with our own Mexica warrior as the playable protagonist while preserving the project's visual identity and existing combat mechanics.

#### 1. The decision to move away from Manny

Manny had served his purpose. His skeleton and native animations allowed us to build and test complete combat: attacks, combos, blocking, parrying, counterattacks, dodging, lock-on, stamina, Rally, and criticals. Without him, the game would not have become playable.

But a mannequin cannot tell our story. Necoc Yaotl needed the character onscreen to be the warrior from the desecrated sanctuary, with his helmet, feather collar, loincloth, and Macuahuitl. Visual identity stopped being an optional polish item and became a requirement.

Milestone 6 helped us find another route, partly by showing what did not work. We had tried to move animations between skeletons without producing an approved retarget, while the 109-bone custom rig—with its controls and IK—was still not production-ready. Instead of forcing animations onto that rig, we did the opposite: **build the character on the 65-bone Quaternius skeleton** used by the Universal Animation Library.

The change sounds small but was not. There would be no transfer between different skeletons: the character would be built on the very skeleton used to create the animations. The 109-bone rig was not discarded as a learning experience or erased from the project; it simply stopped being a prerequisite for the warrior to enter the game.

#### 2. Preparing the warrior in Blender

The playable protagonist was prepared in Blender. **Verified state:**

| Part | Object | Data |
|---|---|---|
| Skeleton | `NY_Prota_Quaternius_Rig_Test` | 65 bones; 86 library actions present in the working scene |
| Body | `NY_Prota_Quaternius_Mesh_Test` | 6,652 vertices, 12,871 triangles, 65 vertex groups (one per bone) |
| Helmet | `NY_Acc_Casco` | 5,514 vertices, 9,477 triangles, one group |
| Feather collar | `NY_Acc_Collar` | 6,537 vertices, 10,132 triangles, seven groups |
| Loincloth | `NY_Acc_Faldin` | 6,911 vertices, 13,260 triangles, four groups |
| Macuahuitl | `NY_Acc_Macuahuitl` | 5,689 vertices, 9,605 triangles, no skinning (independent weapon) |

We adapted the protagonist's geometry to the Quaternius rig and built skinning so that the body could receive the library's animations **without retargeting**: the same skeleton that authored the animations drove the mesh. The body had one vertex group per bone, so actions could play without skeleton conversion.

Accessories remained separate to preserve both their visual appearance and their individual weights and materials. Helmet, collar, and loincloth were not fused into the body; in Unreal, they followed its pose as independent meshes. The Macuahuitl was also separate, as a standalone weapon.

The proportions and Mexica identity—silhouette, helmet, feathers, loincloth—were deliberately preserved. Visual approval belonged to the director (**REPORTED BY THE DIRECTOR**).

#### 3. Integration in Unreal Engine 5.8

**Verified game assets:**

| Asset | Role | Data |
|---|---|---|
| `SK_Protagonist` | Skeleton | 65 Quaternius bones plus root armature node |
| `SKM_Protagonist_Body` | Skeletal Mesh | Body |
| `SKM_Protagonist_Casco` | Skeletal Mesh | Helmet accessory |
| `SKM_Protagonist_Collar` | Skeletal Mesh | Collar accessory |
| `SKM_Protagonist_Faldin` | Skeletal Mesh | Loincloth accessory |
| `SM_Macuahuitl` | Static Mesh | Independent weapon |
| 57 `AS_*` | Animation | Library AnimSequences |
| `BS_Protagonist_Locomotion` | Blend Space | Idle/Walk |
| `ABP_Protagonist` | Animation Blueprint | Animation logic |
| 4 `M_Protagonist_*`, 16 `T_Protagonist_*` | Materials and textures | PBR resources |

The imported hierarchy preserved the armature node in addition to the 65 bones (66 entries). This was not merely cosmetic: that node later caused the scale problem.

Accessories were integrated as independent `SkeletalMesh` components attached to the body and synchronized using **Leader Pose** (`SetLeaderPoseComponent`). Each kept its own skinning weights but copied the body's pose: helmet, collar, and loincloth followed protagonist animations without merging geometry or recalculating weights (**VERIFIED in implementation code**).

The weapon followed a different path. `BP_Weapon_Macuahuitl` remained an independent actor containing `SM_Macuahuitl`, attached to the hand when equipped. The combat system consumed the weapon actor as before; attack DataAssets still used temporary stick-weapon settings (`DA_Stick_*`), an inherited debt from Milestone 6.

#### 4. The 100:1 scale problem

This technical problem cost us the most time to understand because its symptoms were misleading.

When importing from Blender into Unreal, the armature node produced a hierarchy with an **inherited scale of 100**. The character itself looked right: mesh properly positioned, proportions correct, animations playing. But anything attached to a bone inherited that scale.

Why did the mesh look right while attachments failed? Skinning is evaluated in bone space: deformation depends on hierarchy and weights, rather than directly on the root node's scale. A character with a root at scale 100 can appear normal. An actor attached to a bone—the Macuahuitl—inherits the component transformation, including the scale that skinning hides from view. The result was a gigantic, displaced weapon on a seemingly normal character.

We corrected it in two explicit code steps:

1. Attach the weapon using `SnapToTargetNotIncludingScale`, preventing it from inheriting bone scale.
2. After applying the relative transform, force the actor's world scale to one (`SetActorScale3D(FVector::OneVector)`).

The fix is idempotent: if the skeleton is eventually corrected to scale one, the weapon will still have the right size. The code explicitly records a debt: **the imported skeleton root retains scale 100**. We fixed the weapon, not the underlying source of the problem.

The final Macuahuitl placement was adjusted manually by the director until it sat correctly in the hand (**REPORTED BY THE DIRECTOR**). The approved transform was `offsetLoc=X=-0.08, Y=0.01, Z=0.01` and `offsetRot=P=60.52, Y=-47.89, R=-155.88`. A revealing warning remained: the weapon's declared `HandGrip_R` socket **does not exist** on the imported mesh, so attachment falls back to `hand_r` and the offset was calibrated against that bone. Creating the socket remained **PENDING**.

An uncomfortable but useful lesson followed: **successful asset import does not guarantee correct transforms**. Checking the real root-node scale, socket existence, and weapon world dimensions costs less than discovering the problem with an enormous weapon stretching across the screen.

#### 5. First locomotion of the new character

With body, accessories, and weapon in place, the protagonist began moving on his own skeleton. The first implementation was deliberately simple: `BS_Protagonist_Locomotion` provided Idle/Walk and was played in single-node mode if the mesh had no Animation Blueprint. If `ABP_Protagonist` was assigned, the code respected it and did not replace it (**VERIFIED**).

It was a first locomotion pass, not the final one. It was enough to check that the character moved, accessories followed, and the weapon stayed in the hand. Full integration of `NY_` animations belonged to later milestones.

#### 6. Problems, decisions, and lessons

- **An imported mesh is not a playable character.** It still needs the correct skeleton, weights, accessories, weapon, locomotion, and gameplay validation.
- **Skeleton, animation, and accessory compatibility.** The body used `SK_Protagonist`; library animations played on that skeleton; accessories followed via Leader Pose. All three depended on the same contract.
- **Attachments and transforms.** The 100:1 problem demonstrated that an attachment can fail even when the character looks fine.
- **Preserve combat mechanics.** The new character reused existing combat, inventory, lock-on, and critical components; we did not rewrite combat just to change the model.
- **Separate technical checks from visual approval.** An agent can verify counts, hierarchies, weights, logs, and transforms. The director determines whether the warrior actually *feels* like the protagonist of Necoc Yaotl while playing.

**Verified technical facts:** the playable rig had 65 bones and 86 actions in the Blender working scene; the body contained 6,652 vertices and 12,871 triangles. Unreal contained the body, three accessories, four protagonist materials, sixteen textures, 57 animation sequences, locomotion, and an Animation Blueprint. PIE logs confirmed world scale 1.00 for the weapon while also recording the missing `HandGrip_R` socket and fallback to `hand_r`. The latest Git checkpoint during this stage was `21a5156` (November 14, 2026), before this integration was committed.

**Evidence limitations:**

- Visual PIE validation belonged to the director; no screenshot or video of this stage was available in the project history.
- The skeleton-root scale was compensated for in code, not structurally fixed.
- `HandGrip_R` did not exist; the weapon used `hand_r` and a manually calibrated offset.
- Attack DataAssets still came from the test stick (`DA_Stick_*`).
- Full integration of `NY_` and final combat animations did not belong to this milestone.

**Result:** Necoc Yaotl stopped depending on Manny visually. The game now had its own protagonist—body, helmet, collar, loincloth, and Macuahuitl—integrated into Unreal Engine 5.8, animated on its own skeleton with basic locomotion working. It was not the finished character, but it was *our* character.

**Development reflection:** during Milestone 6, animation felt like a wall. This milestone did not break the wall; it found another route. We stopped trying to force our character onto a different skeleton and instead built him around a skeleton that already had animations. That decision, the artistic work, and a great deal of patience with transforms brought the warrior to life.

It also confirmed what we had begun to learn: character problems do not end when a mesh looks right. They end when the character moves, the weapon stays in the hand, accessories follow the animation, and combat continues working. That is when a mesh stops being merely a file and starts becoming a character.

DeepSeek V4.1 Flash through OpenCode helped prepare the character, export/import pipeline, materials and textures, transform diagnoses, and technical checks. ChatGPT supported planning and analysis. The director owned artistic direction, final weapon positioning, visual identity, and approval.

---
### Milestone 9 — From Graybox to Mexica Temple

> **Evidence note.** This milestone follows the director's recorded chronology: asset names, counts, and elevations come from that period and were not independently reaudited for this text. We distinguish what was **imported and integrated** from what was **designed or proposed**, and what was **geometrically verified** from what still required visual approval.

**Goal:** transform the functional `L_RitualDungeon_Graybox` dungeon into a dark fantasy temple with Mesoamerican identity while preserving the playable layout supporting combat, AI, and navigation.

#### 1. Starting point

`L_RitualDungeon_Graybox` began in Milestone 5 as a laboratory: ritual chamber, corridors, plaza, side rooms, provisional boss room, enemies, and NavMesh. It worked, and that was precisely the problem: it looked like a test box.

We could have rebuilt it. The director decided instead to **keep the playable layout** and dress it. Graybox geometry would continue defining routes, encounters, and distances; the space's visual identity would change.

This decision guided everything afterward: each new element had to fit the already playable level, not the other way around.

#### 2. Architectural identity

We developed visual concepts and resources: stone walls with Mesoamerican motifs, ornamental columns, modular floors and roofs, reliefs, murals, statues, and ceremonial braziers.

Not every idea made it into the level, and artistic direction mattered as much as the individual assets:

- The director **rejected walls with holes** and asked for completely solid surfaces. A perforated wall may read as a ruin, but it breaks a temple's visual continuity and complicates lighting and collision.
- **Floor and ceiling designs** were deliberately simplified to avoid excessive ornament. In a temple, too much detail competes with the silhouette and readability of combat.
- We standardized texture and material naming around **`BaseColor`**, rather than `Albedo`, to match Unreal's terminology.

These were **concepts and direction criteria**. The assets actually integrated during the stage are described next.

#### 3. Models and materials

Two key pieces were integrated after passing the import pipeline developed in Milestone 7:

| Asset | Triangles | Dimensions (cm) |
|---|---|---|
| `SM_Temple_Pillar_01` | 9,427 | 108.54 × 108.84 × 299.85 |
| `SM_Bracero` | 10,770 | 95.46 × 94.09 × 99.95 |

We also worked with the **Tezcatlipoca statue**, an asset developed for Necoc Yaotl during the jam and integrated at an earlier point in the same development process.

Problems appeared when placing these pieces in the temple:

- **FBX scale and units.** A model can look coherent in its originating tool and arrive in Unreal at an unusable scale. Interpreting units became a mandatory step before level placement.
- **PBR materials.** Connections matter: BaseColor and Normal through color channels; **Metallic and Roughness as linear data**. Reading the latter as color prevents surfaces behaving correctly as stone or metal.
- **Textures failing to display.** At times a texture existed and the material was wired, yet the mesh looked flat or gray. The cause lay in sampler configuration and color space, not the underlying file.

The practical lesson: an imported material is not a finished material; it must be inspected on the mesh under level lighting. We applied the pipeline developed in Milestone 7.

#### 4. Fourteen pillars

The director **manually positioned 14** `SM_Temple_Pillar_01` pillars at **uniform scale 1.75**. Their reference top elevation was **`Z = 524.7437 cm`**.

This was not arbitrary: it was the actual pillar-top height in the level, and it became the datum for subsequent architecture. Pillars were arranged around existing walls, passages, and the established route, rather than according to a theoretical floor plan.

A crucial decision followed: **build the roofs around existing pillar and wall positions**, without moving them or changing the playable layout. The architecture would adapt to the level, not vice versa.

#### 5. The roof

With reference geometry defined, the roof system was assembled from **38 new elements**:

- **17 slabs** covering the chambers.
- **19 bands** finishing the tops of walls.
- **Two transition panels** bridging changes in height.

Three reference heights were used: **500 cm**, **524.7437 cm**, and **800 cm**. The middle matched the pillars; the tallest was reserved for the temple's highest space.

We preserved the **raised porch** to avoid blocking the **Fog Gate**. Closing the roof could not obstruct the ceremonial entrance or obscure the approach to combat.

Placement was not based solely on visual guesswork: **165 geometric coverage checks** verified that elements covered their intended areas without gaps or overlaps. The map's actor inventory increased from **145 to 183 actors**.

Geometric verification proves coverage, not visual quality. Whether the room actually looks right is a separate judgment made by the director in the level.

#### 6. Problems and decisions

- **Turning a working level into an artistic space** costs more than expected because it already contains gameplay decisions that art must respect.
- **Modularity was the solution.** Reusing a limited set of pieces many times dresses a large level without multiplying assets or losing consistency.
- **Surface continuity.** Solid walls, bands, and slabs must meet without visible gaps or steps; that is where good architectural planning becomes apparent.
- **Scale and orientation.** A properly imported piece can still be placed incorrectly; scale, pivot, and rotation are checked in context.
- **Roofing changed the lighting requirements.** Open spaces and enclosed interiors need different light, so an architectural choice demanded lighting changes.
- **Navigation, combat, and enemies were preserved.** This was architectural work, not a gameplay redesign: NavMesh, encounters, and AI remained on the same layout.
- **Implementing does not mean verifying.** Placing 38 actors and checking coverage proves the geometry exists; making the room read as a temple requires human visual approval.

#### 7. AI collaboration

- **ChatGPT (OpenAI):** planning, analyzing alternatives, technical coordination, reviewing proposals, and supporting architectural decisions.
- **DeepSeek through OpenCode:** authorized technical implementation, asset creation/configuration, task automation, geometric checks, and reports.
- **Director of Yaxché Industries:** artistic vision, pillar design and placement, material/model selection, scope decisions, approval of plans, and visual validation.

**Evidence and limitations:** the director provided the figures recorded above: dimensions and triangle counts for the pillar and brazier, 14 pillars scaled to 1.75 with tops at Z = 524.7437 cm, 38 roof parts (17 slabs, 19 bands, two transitions), reference heights of 500/524.7437/800 cm, 165 coverage checks, and the increase from 145 to 183 actors. `BaseColor` naming and corrections to samplers and linear Metallic/Roughness were adopted during this phase. Later imports of `Mural3`/`Mural4`, the final Conquistador, and the 47 `NY_` animations are **not** claimed as results of this milestone. No additional dates, commits, or screenshots were invented. Visual approval of the temple belonged to the director.

**Result:** Necoc Yaotl stopped looking like a generic graybox dungeon. The level kept its playable layout while acquiring an architectural identity: ceremonial pillars, stone walls, modular ceilings, and a recognizable boss entrance.

**Development reflection:** art direction transformed a technical structure into a narrative space. The graybox did not disappear; it was dressed. Every pillar, slab, and band depended on existing geometry, and the restriction against moving it forced us to think of the temple as architecture rather than stage decoration.

It also became clear that art cannot simply be left until the end: adding the roof changed the lighting, and lighting changed the whole level. Recording those dependencies is as much a part of development as placing the pieces.

---

### Milestone 10 — Forty-Seven Animations and the Battle Against Scale

> **Evidence note.** As in previous milestones, **VERIFIED** refers to checkable technical/file data, **REPORTED BY THE DIRECTOR** to decisions and experiences not accompanied by a formal report, and **PENDING** to unfinished or unvalidated work. This milestone follows the director's chronology; the entire project state was not reaudited to prepare it.

**Goal:** stop relying on Manny's provisional movements and begin using the warrior's own animations directly in his Animation Blueprint and actual gameplay.

#### 1. Starting point

In Milestone 8, the Mexica warrior had been integrated using the Quaternius skeleton. At the end of that stage there were `SK_Protagonist`, 57 `AS_*` animations, `BS_Protagonist_Locomotion`, `ABP_Protagonist`, and the Macuahuitl and accessories linked to the character.

However, having animation assets in Unreal does not mean game actions use them. The character could move and looked correct; what remained was linking his own animations to real combat states.

Our goal was precisely that: replace temporary movements with Quaternius animations without damaging the combat system that already worked.

#### 2. Preparing and importing the 47 animations

We prepared the chosen Quaternius actions in Blender and exported them as **47 individual animation FBXs**. Each was imported into Unreal as an AnimSequence using the `NY_` naming convention and associated with `SK_Protagonist`.

The process followed Milestone 8's approach: use the same Quaternius skeleton and preserve names and associations. Before accepting an import, we checked that the file loaded, targeted the correct skeleton, had the expected name, and contained animation data.

Two collections must not be conflated:

- **57 `AS_*` sequences** imported during the protagonist's initial integration.
- **47 `NY_*` sequences** individually exported from Blender in this stage.

That does **not** prove there were 104 distinct animations. Content could overlap, and simply adding the counts would make an unverified assumption.

#### 3. Unexpected animation durations

Inspection exposed an uncomfortable issue: **seven animations with fractional or unexpected durations**.

This was not cosmetic. Odd durations can indicate an extra keyframe, an incorrect export range, or a final frame stretching the sequence. It again demonstrated the difference between four things we casually call “animation”:

1. An asset present in the Content Browser.
2. An FBX with coherent frames and duration.
3. An animation that plays correctly on the character.
4. An animation connected to gameplay through transitions and montages.

The seven cases were recorded as detected issues. We do not invent names or exact durations that were not in the record, nor claim that all seven were corrected. Confirmed fixes are described where supported; full closure remained pending.

#### 4. The return of the 100:1 problem

Scale returned. In Milestone 8, we had compensated for the Macuahuitl inheriting bone scale, but fixed the weapon rather than the cause.

As we began using `NY_` animations, the inherited root-node scale appeared again, now affecting character transforms and animation playback rather than only an attachment.

We followed our established method: reproduce, isolate, compare. We examined scale effects on the skeleton, sequences, and Animation Blueprint, discarding explanations that focused only on the weapon. The character needed **compensation in the animation system itself**, not another weapon patch.

These interventions must be distinguished:

- **Milestone 8:** correction of the attached weapon's scale.
- **Milestone 10:** compensation for scale in the animation system and Animation Blueprint.

Compensation should not be confused with a cure. It can allow a character to look and move correctly without fixing the source file or Skeleton root. The structural problem remained technical debt.

#### 5. Integration into ABP_Protagonist

We integrated animations incrementally, starting with constant needs:

- Idle and locomotion.
- State transitions.
- Combat movements.
- Dodge, roll, and dash where relevant.
- Compatibility with existing combat montages.

Initially **eight `NY_` animations were connected** to the system. Eight, not forty-seven: the rest remained in the library until integrated and validated.

A critical technical requirement was preserving **`DefaultSlot`**. Attack montages play through that slot. Blocking or replacing it in the ABP would stop combat animations from appearing. Every ABP change had to respect this contract.

#### 6. Regressions and corrections

Integration was not linear. Several symptoms appeared, sometimes looking alike despite different underlying causes:

- Incorrect transforms caused by scale.
- Animations interfering with one another.
- States preventing certain animations from playing.
- The protagonist intermittently disappearing.
- Conflicts with idle updates.

Each symptom required separate investigation and hypothesis testing. One documented correction was **disabling `TickLockedIdle()`** when it competed with the new system. This was not about “fixing idle”; it removed logic that conflicted with the ABP.

The rule was simple: small reversible changes, with verification after each. Fixing one regression by breaking another system is not a fix; it creates new debt. We did not claim all problems were resolved: visual validation of transitions and combat came later.

#### 7. AI collaboration

- **ChatGPT (OpenAI):** integration planning, Blender–Unreal compatibility analysis, alternative approaches, scale diagnosis, and correction coordination.
- **DeepSeek through OpenCode:** authorized task preparation, implementation, import, integration, static checks, diagnosis, and reporting.
- **Codex (OpenAI):** targeted technical collaboration on diagnosing and compensating for scale in the Animation Blueprint, distinct from DeepSeek/OpenCode's work.
- **Director of Yaxché Industries:** selection of priority movements, approval of plans and scope, detection of errors during playtests, exclusive visual validation, and decision to protect working combat instead of rebuilding it.

#### 8. Problems, decisions, and lessons

- **Importing 47 animations does not mean 47 playable actions.** An animation library is raw material; gameplay integration is another layer.
- **A shared Skeleton does not guarantee correct transforms.** Scale and hierarchy still matter.
- **Scale compensation can resolve a symptom without solving its cause.** Technical debt should be acknowledged rather than hidden.
- **An Animation Blueprint must preserve existing montage contracts.** `DefaultSlot` is essential to combat playback.
- **Regressions require small, reversible changes.** Isolate, test, and roll back when necessary.
- **An agent's responsibility ends at technical verification.** Visual approval belongs to the director; this prevented unfinished results from being called complete.

#### 9. State at the end of the milestone

**Technically completed:**

- Imported 47 `NY_` animation sequences.
- Connected an initial subset of eight animations.
- Worked on scale compensation in the animation system.
- Preserved `DefaultSlot`.
- Made incremental Animation Blueprint fixes.

**Pending or awaiting validation:**

- Full integration of the library.
- Visual evaluation of every transition.
- Deformation quality during combat.
- Confirmation that abnormal-duration cases were resolved.
- A final structural fix for Skeleton scale.

Not all combat and stealth movements were presented as finished.

**Evidence and limitations:** `SK_Protagonist`, `ABP_Protagonist`, the `NY_` animation collection, and the import, duration, and scale observations formed the basis of this milestone. The number of 47 sequences and seven abnormal durations are **REPORTED BY THE DIRECTOR** where no independent report was incorporated. No commits, dates, individual durations, logs, or visual successes were invented. Scale compensation and disabling `TickLockedIdle()` were recorded as agent-reported technical changes, not visual approvals.

**Result:** the protagonist began to move using his own animations rather than borrowed Manny sequences: 47 imported sequences on his skeleton, an initial set connected to the Animation Blueprint, and existing combat preserved. It was not the entire library functioning in gameplay, but ownership of the movement had changed.

**Development reflection:** this stage was less visually dramatic than the previous one and more uncomfortable. Importing animation is fast; making the character use it without breaking anything takes time. Scale returned to remind us that a compensated problem still exists, and odd durations forced us to distinguish “visible in the Content Browser” from “working in game.”

The director's most useful decision was to preserve the existing combat before attempting to rebuild it. Under that constraint, every new animation had to coexist with existing montages, `DefaultSlot`, and tested states. Less freedom, but far less risk.

---
### Milestone 11 — Racing the Clock: Agents, Regressions, and Combat Refinement

> **Evidence note.** As above, **VERIFIED** means checkable technical/file data, **REPORTED BY THE DIRECTOR** means a recorded decision or experience without a formal supporting report, and **PENDING** means unfinished or unvalidated work. The director supplied this phase's chronology; the whole project was not reaudited for this account.

**Goal:** stabilize the existing character and combat, integrate the animation library without breaking mechanics, and recover validation time during the final stretch of the MegaJam.

#### 1. Starting point

We entered this stage with essentials in place: the integrated Mexica warrior, `SK_Protagonist` and `ABP_Protagonist`, 47 imported `NY_` animations, an initial set of eight connected, and a combat system that already worked.

The problem shifted from “what do we add?” to “what are we breaking?” Each new integration touched a working system, and the final stretch left no time to rebuild.

#### 2. Integration grows more complex

Work was distributed across fronts that could not advance independently:

- Locomotion and transitions.
- Jumping.
- Stealth and crouched movement.
- Roll and dash.
- Attacks and montages.
- Criticals and special actions.

In an Animation Blueprint these share states, transition rules, and slots. Improving a jump transition might trap the character in a state, prevent a montage from playing, or break the return to Idle after attacking.

That was the uncomfortable discovery: **an apparently small change could affect several parts of the AnimGraph at once**. Integration was no longer simply adding animations; it became a coordination problem.

We do not claim all these integrations received visual approval. Work was attempted; validation is a separate matter.

#### 3. Regressions

Milestone 10 covered the technical origins of several problems. Here, their consequences mattered:

- **Intermittent protagonist disappearance.** A symptom that did not always occur in the same location and forced investigation of transforms, scale, and state.
- **100:1 scale problems.** The inherited root node reminded us that compensation can work without curing the source.
- **Animations incompatible with certain states.** Clips correct in the library could still conflict with the states in which playback was attempted.
- **Conflicts among Idle, locomotion, and montages.** The character could become stuck in an animation or return to idle at the wrong time.
- **Risk of breaking attacks by changing AnimGraph.** Graph changes could block combat montages.
- **Corrections creating new symptoms.** The familiar pattern: fix jumping, break dodging.

Two elements were essential: preserving **`DefaultSlot`**, the path through which montages play, and disabling **`TickLockedIdle()`** when its logic competed with the new animation system. Both had appeared in Milestone 10, but here they were understood as parts of ongoing stabilization rather than isolated tweaks.

#### 4. Codex joins the development process

This was the milestone's central organizational event.

Until then, **DeepSeek V4.1 Flash through OpenCode** had been the primary implementation agent. As integration grew more complex, the director added **OpenAI Codex** as a second technical agent.

Its arrival required configuring access to the project and **Unreal MCP**, allowing Codex to inspect and interact with the editor under the same safeguards used for other agents. Its work included:

- Reviewing `ABP_Protagonist`.
- Investigating scale issues.
- Analyzing animation regressions.
- Applying technical corrections to the animation system.
- Protecting existing mechanics and assets.

We must distinguish investigation from implementation: not everything reviewed became a code change, and not every applied change was visually validated. The record maintains that distinction.

**Codex did not replace DeepSeek.** Both participated in specific technical roles under human direction. The organizational lesson was moving from reliance on one agent to coordinated specialists with defined scopes and explicit approvals.

#### 5. The importance of change control

With multiple agents and a fragile system, our process became essential:

`PLAN → approval → BUILD → technical check → director's validation`

In practice, this meant:

- **Incremental changes**, one at a time, so causes remained identifiable.
- **Rollbacks** when a fix failed; reverting was no longer treated as failure.
- **Combat-system protection:** no animation change could disable attack montages.
- **Closed scope:** a request for one transition was not permission to reorganize the entire graph.
- **Evidence before success claims:** successful compilation does not prove correct appearance.
- **Compilation versus behavior:** compilation is a condition, not the result itself.

One explicit rule emerged: **agents must not run PIE, capture images, or conduct automated visual tests**. Playable and visual validation belonged solely to the director. Agents compiled, inspected, diagnosed, and reported; the director played, watched, and decided.

#### 6. Refining combat feel

While agents worked on stability, the director continued directly refining how combat felt. This was not blind numerical tuning but constant attention to:

- Attack rhythm and weight.
- Responsiveness of actions.
- Transitions between movement and combat.
- Impact feel.
- Enemy behavior in encounters.

This work is difficult to express numerically because its acceptance criterion is a feeling. **Refinement was ongoing** and was not declared finished; it was a natural part of both the genre and the jam's final stretch.

#### 7. Turning off visual debug

The director confirmed that **the game's visual debug display had been disabled**.

During AI development, visual tools had been indispensable for understanding perception, navigation, and abandoned pursuits. During combat refinement, these overlays became an obstacle: we wanted to judge the experience without diagnostic indicators covering the screen.

Crucially, **the debug system was not deleted**, only its visualization was turned off. The underlying tools remained available for later diagnostics.

#### 8. AI collaboration

- **ChatGPT (OpenAI):** planning, problem analysis, architectural review, agent instruction coordination, prioritization of corrections, and protection of existing systems.
- **DeepSeek V4.1 Flash through OpenCode:** technical implementation and integration, code and Blueprint review, compilation, diagnosis, reports, and authorized fixes.
- **Codex (OpenAI):** new technical agent with Unreal MCP access, investigation and correction of Animation Blueprint and scale problems, support for animation stabilization.
- **Director of Yaxché Industries:** technical and creative direction, prioritization, approval of plans and fixes, identification and assessment of regressions, hands-on combat-feel refinement, exclusive visual validation, and decision to disable debug overlays.

#### 9. Problems, decisions, and lessons

- **More agents do not necessarily mean faster progress.** Without coordination, more contributors can make conflicting changes to the same system.
- **Defined responsibilities are essential.** Each agent needs scope and approval.
- **A successful compile does not prove an animation works.** Compilation and appearance are separate checks.
- **Regressions can cost more than new features.** Protecting what works is active work, not inertia.
- **Combat must feel right, not merely execute correctly.** Several mechanically correct systems can still combine into an unsatisfying experience.
- **Human direction determines which problems to solve now.** In a jam, that prioritization is the difference between shipping and running out of time.

#### 10. Historical state

**Documented progress:**

- Codex added to development.
- Technical work on Animation Blueprint integration and regressions.
- Incremental corrections to protect animation and combat.
- Direct combat refinement by the director.
- Visual debug turned off.

**Pending:**

- Full visual animation validation.
- Confirmation that regressions were completely resolved.
- Final transition polish.
- Combat validation with definitive character models.
- Further combat-feel improvements.

The game was not finished at this stage. This milestone is about maintaining and polishing the working base, not claiming completion.

**Evidence limitations:** the technical work involved `ABP_Protagonist`, `SK_Protagonist`, `NY_` animations, `DefaultSlot`, `TickLockedIdle()`, and Codex's Unreal MCP setup. Diagnoses and fixes not independently verified here remain **REPORTED BY THE DIRECTOR / AGENTS**; no undocumented outcomes are treated as proven. Stabilization was recorded as technical work, not visual proof.

**Result:** development entered its stabilization phase with a more carefully managed animation system, an additional technical agent, and one clear rule: only the director validates visually. Combat continued to improve while debug overlays no longer obstructed the screen. The race against time was won through less noise, not more features.

**Development reflection:** this milestone is about sustaining, not adding. A good agent pipeline is not the one that produces the most changes, but the one that can safely revert one and explain what broke. We also learned that combat is not finished when it compiles: it is finished when it feels right, and that judgment cannot be automated.

---

### Milestone 12 — Birth of the Conquistador

> **Evidence note.** This section distinguishes **VERIFIED** (checkable file or technical report), **REPORTED BY THE DIRECTOR** (decision or experience), and **PENDING** (unconfirmed or unvalidated work). The director supplied this stage's chronology; the project was not reaudited to write it.

**Goal:** give the invaders a distinctive visual identity and a final enemy model that could leverage the protagonist's animation system without creating an entirely separate skeleton pipeline.

#### 1. Starting point

The Mexica protagonist was already in Unreal. Enemies, however, were still using provisional models: they were sufficient for AI and combat testing, but did not visually represent the story's invaders.

The director decided to prepare a **definitive Conquistador model in Blender**, adapted to the same Quaternius skeleton as the protagonist. There were two reasons: visual identity and reuse of the established animation system.

#### 2. Preparation in Blender

**Verified properties of the prepared enemy:**

| Element | Data |
|---|---|
| Mesh | `EnemyBase` |
| Armature | `NY_Enemy_Quaternius_Rig_Test` |
| Bones | 65 Quaternius |
| Vertices | 5,548 |
| Triangles | 9,726 |
| Materials | 1 |
| UV channels | 1 |

Adapting the character to the rig required both artistic and technical work, including a scope decision: **do not use the original 109-bone Tripo Conquistador rig directly**. That skeleton belonged to the experimental path described in Milestone 6; using it in the game would have required another animation and retargeting pipeline. Instead, we adapted the model to the 65-bone skeleton the game already used.

We excluded `Icosphere.002`, auxiliary geometry not belonging to the character. The original Blender file was preserved during export; work was performed on a temporary copy in memory.

#### 3. Sharing the Skeleton

Before exporting, we compared the protagonist's and Conquistador's skeletons. The result was what we had hoped for:

- **65 bones with matching names and hierarchy.**
- Minor differences in rest pose.
- Unreal's imported Skeleton contained **66 entries** because of an additional root armature node.

We chose to reuse `SK_Protagonist`: **no second Skeleton and no unnecessary retargeting**. An enemy sharing the protagonist's skeleton can use its animations without conversion.

However, **structural compatibility** (names, hierarchy, count) had been verified, while the **visual quality of every deformation** still required testing by the director. Sharing a skeleton does not guarantee that every animation looks good on every body.

#### 4. Exporting and importing the enemy

The character was exported from a temporary Blender copy. Necessary transforms were normalized first to **avoid another 100:1 scale problem**, applying lessons from earlier milestones.

**Result in Unreal:** `SKM_Enemy_Base` was imported with:

- Height: **183.84 cm**.
- Skeleton: `SK_Protagonist`.
- **9,726 triangles**.
- One LOD.
- One material.

`M_Enemy_Base` and **four PBR textures** were imported alongside the mesh. The protagonist's existing mesh, Skeleton, and animations were not altered.

#### 5. Three other models

The same operation brought in three more pieces:

| Asset | Triangles | Dimensions (cm) |
|---|---|---|
| `SM_Mural3` | 11,337 | 99.95 × 24.17 × 55.71 |
| `SM_Mural4` | 10,359 (in Unreal) | 99.95 × 17.14 × 34.23 |
| `SM_Consumible` | 10,902 | 16.72 × 4.97 × 20.99 |

All three had four PBR textures, a material, and convex collision. The consumable was an **independent 3D model**, not to be confused with the `NY_Consumible` animation: they shared a name but were different resources.

**24 new assets** were saved, increasing the project's inventory from **185 to 209**.

#### 6. Integrating the enemy into gameplay

Importing a Conquistador does not automatically make it a functioning adversary. After import, **Codex** was tasked with replacing existing enemies' temporary models, equipping them with a sword, and using compatible animations from the protagonist.

The instruction was explicit:

- Preserve AI and combat.
- Do not move or duplicate enemies.
- Reuse `SK_Protagonist`.
- Preserve existing mechanics.
- Adjust visual scale only if necessary.
- Attach a sword to the corresponding hand.

**The result of that BUILD and its visual validation were not part of this historical phase.** Integration was **assigned and pending** at that point in the timeline. Its later progress is described in Milestone 13; this earlier milestone does not retroactively claim completion.

#### 7. AI collaboration

- **ChatGPT (OpenAI):** planning, pre-implementation review, compatibility decisions, risk management, and implementation instructions.
- **DeepSeek through OpenCode:** technical inspection of four models, skeleton comparison, export/import, materials, and static checks.
- **Codex (OpenAI):** subsequently assigned the integration of the Conquistador's enemy behavior and sword; completion was **pending confirmation at this milestone**.
- **Director of Yaxché Industries:** artistic preparation and design of the invader, approval of the process, and exclusive responsibility for visual validation.

#### 8. Problems, decisions, and lessons

- **Sharing the skeleton** avoided a second pipeline and allowed the enemy to use animations already integrated. It was a cost decision, not just convenience.
- **Structural compatibility is not visual compatibility.** Matching names, hierarchy, and count may still yield imperfect deformations; rest pose and weights affect the result.
- **The 100:1 issue was avoided procedurally** by normalizing transforms before export rather than repairing them afterward.
- **We protected the protagonist's assets.** Its mesh, Skeleton, and animations were left untouched; a new enemy should not endanger a working protagonist.
- **Importing an enemy does not make it an adversary.** Behavior integration, weapon attachment, and gameplay validation are separate work.
- **Selective saving and verification.** Only created assets were saved and checked; we did not rely on `Save All`.

#### 9. State and recorded evidence

**Technical results recorded at this stage:** four imported models (`SKM_Enemy_Base`, `SM_Mural3`, `SM_Mural4`, `SM_Consumible`), 24 new assets, materials, textures, collision, and skeleton compatibility. The asset inventory grew from 185 to 209. These are technical results, not confirmation of final playable integration.

**Pending at the end of this milestone:** confirmation of Codex integration, equipped sword, animation appearance, and Conquistador combat testing.

No unrecorded results, commits, dates, or screenshots are invented.

**Result:** the invaders gained a definitive visual model rather than a temporary mannequin. The Conquistador shared the protagonist's Skeleton and was prepared to inherit its animation system. What was still missing in this milestone was evidence of it fighting.

**Development reflection:** this phase taught us about limits. Adapting a character to an existing skeleton cost less than opening a second rigging pipeline; sharing `SK_Protagonist` avoided duplicating animations and decisions. But importing a correct enemy model is not the same as finishing an adversary: there is still a BUILD, a sword in the hand, and director-led visual validation between those states.

---
### Milestone 13 — The Final Countdown

**Closing date: November 15, 2026.**

> **Editorial and evidence note.** Milestones 1–12 are preserved as historical records, including what was pending and the decisions made at the time. This final milestone explains what happened afterward; it does not retroactively rewrite them. Animation, environment, and combat work overlapped, so the order of these sections does not claim an exact hour-by-hour timeline. **VERIFIED** identifies technical details checked during development; **REPORTED BY THE DIRECTOR** identifies his tests, decisions, and publication confirmations; **PENDING** denotes what was not established. Compiling, saving, packaging, and playing are different levels of verification. This journal is self-contained and does not require separate evidence documents to follow the narrative.

**Goal:** turn the integration that was still assigned at the end of Milestone 12 into a distributable Windows submission without rebuilding combat or confusing the end of a jam with the completion of every original idea.

#### 1. The Conquistador enters the temple

The integration left pending by Milestone 12 continued during the jam. All **16 `BP_Enemy` instances already present at this stage of development** were updated to use `SKM_Enemy_Base`, `M_Enemy_Base`, and an enemy-specific Animation Blueprint, `ABP_Conquistador`. Their transforms and the existing detection, pursuit, damage, collision, and lock-on architecture were preserved. No new enemy actors were duplicated merely to simulate an integration.

The enemy reused `SK_Protagonist`, but not `ABP_Protagonist`: its locomotion used the owning Character's horizontal speed and did not depend on player-specific states. Technical verification covered `NY_Sword_Idle`, `NY_Walk_Loop`, `NY_Sword_Attack`, `NY_Death01`, and reactions `AS_Hit_Chest`, `AS_Hit_Head`, and `AS_Hit_Knockback`, while preserving `DefaultSlot`. This also clarifies scope: integrating priority `NY_` animations did not mean replacing every compatible `AS_` animation or connecting all 47 sequences as different gameplay actions.

Transform compensation was calculated from the actual enemy data: approximately **93.534935** as an upper scale factor and **7.254858 cm** of vertical translation, instead of copying the protagonist's value of 100. The pose chain and sword attachment to `hand_r` were checked, with a world scale independent of inherited bone scale and no additional weapon collision that might create a second damage system.

The director spotted the sword being held by its tip. A targeted correction followed: a 180-degree Roll rotation and recalculated translation around the grip point. The technical work included checks across all 16 instances, although fine visual approval of hand placement and poses remained the director's responsibility.

Next, the existing boss actor received `SKM_Boss_Base`, `ABP_Boss_Base`, and `SM_EspadaBoss`. The resulting recorded level contained **15 Conquistadors and one boss**—not 16 Conquistadors plus an extra enemy. The actor already referenced by the encounter was retained, and a boss-specific upper scale factor of 100 was calculated without changing the shared Skeleton.

Blueprint compilation and asset saving were checked during integration, but these technical checks **do not amount to recorded combat gameplay or substitute for the director's visual approval**.

#### 2. Animation: protect pose and combat before adding clips

The protagonist's disappearance was not treated as a weapon issue or an excuse to resize the entire character globally. We first restored the functioning AnimGraph and compared transforms between `NY_` sequences and reference `AS_` sequences.

A numerical test uncovered the decisive discrepancy: in Idle, Walk, and Jog, the compared local root and pelvis transforms matched, yet the resulting pelvis height was about one hundred times smaller without compensation. For example, an Idle range of **0.8687–0.8772** became **86.8671–87.7172**, matching the `AS_` reference. This was technical evidence of a scale mismatch; it did not automatically explain every visual symptom seen during regressions.

Adaptation was performed within the animation system while preserving original meshes, Skeleton, and clips. Compensation first checked for locomotion was later moved **after `DefaultSlot`** so it also covered combat montages. The integration process kept **52 protected files unchanged**. Leader Pose and the warrior's accessories were preserved. `TickLockedIdle()` remained disabled.

The eight locomotion sequences were `NY_Idle_Loop`, `NY_Walk_Loop`, `NY_Jog_Fwd_Loop`, `NY_Jump_Start`, `NY_Jump_Loop`, `NY_Jump_Land`, `NY_Crouch_Idle_Loop`, and `NY_Crouch_Fwd_Loop`. Technical checks confirmed connections and compilation; transition quality was not certified by automated visual testing.

There were also specific integration failures:

- **Running changed speed but did not change the animation as expected.** After the director confirmed 600 cm/s in the test, we discovered that changing BlendSpace sample properties did not rebuild the sampling data. The internal BlendSpace was rebuilt from resampled data, and Idle/Walk/Jog, actual speed input, and connections were checked. The director later reported that the result looked right. His approval did not amount to an automated test of every subsequent speed.
- **Roll did not trigger when X was pressed in the old configuration.** We corrected a condition that required a sprint threshold before choosing `NY_Roll`. X was part of that historical diagnostic; the final dodge mapping later moved to Space.
- **Criticals:** `NY_Sword_Attack` replaced `AS_Sword_Regular_C` only along the critical-attack path. The inspected duration was 1.541667 seconds and `CriticalImpactTime` was set to 0.50 seconds. That contact moment was inferred from animation keys and still required visual approval; it was not presented as measured gameplay synchronization.
- **Healing:** `NY_Consumible` was connected to the existing reservation, consumption, and health restoration flow, without creating a second health system.
- **Death:** `NY_Death01`, 2.416667 seconds long, was assigned while preserving one-shot playback, final held pose, and the defeat/retry screen.
- **Combat idle:** `NY_Sword_Idle` required an active lock-on target, near-zero movement, and upright locomotion. Simply carrying a weapon did not trigger it. A small marker was added above the locked target.

Values and controls from earlier stages are not necessarily the final settings; the later changes documented below supersede them.

#### 3. Combat: reverting a regression is also a result

The director's priority was to make combat feel better, not simply increase damage as a substitute for depth. We reused the existing resolver and FSM to extend boss behavior with attack patterns, combos with independent contact windows, guarding, parrying, counters, and contextual criticals. A large boss health bar labeled **“Exploration Boss”** was connected to the encounter's existing attributes.

Technical checks recorded five boss attack patterns and cancellation of remaining contact windows after the relevant interruption. Some heavy-combo timings were inferred from animation keys and remained subject to manual review. Nor do we claim that group combat gained a fully coordinated tactical system: the work described here did not establish one.

Defense tuning preserved the player's **220 ms** parry window and used the existing cooldown to restrict new attempts. Roll had a **250 ms** immunity window, while backstep retained **160 ms**. Those immunity windows did not span the whole animations and also applied against boss criticals. Guard used F at one point in development, but the final control mapping was changed later and is recorded below.

The hitbox review became the clearest case of an incorrect scope decision. The request had been to slightly shorten attacks that appeared to connect from too far away. Instead, the implementation attempted to solve a larger problem by detecting weapon contact against body volumes attached to bones. **The director reported a serious regression: enemies stopped hitting the player.** We removed that integration, restored the earlier combat files, and removed its helper and tests. Those tests are not presented as evidence of playable correction.

The later fix was much smaller: remove only the extra 10% margin from two enemy and boss range comparisons. The documented effective range fell from **242 to 220 cm**. We did not shrink the protagonist's physical capsule or replace the active system with body hurtboxes. Restoring the earlier implementation and applying the small range trim were supported by recorded compilations; final hit feel remained subject to the director's playtests.

The lesson was not “the complex system was almost finished,” but **that we should never have replaced a small urgent adjustment with a riskier new integration**. Slow responses, confusing explanations, and progress updates that failed to distinguish an edit from a testable result also cost valuable time.

#### 4. Finishing the temple: light, fire, complete geometry, and performance

Environment work continued within the existing level layout: complete murals along walls, filler pieces, and modular panels across surfaces. The director identified an important difference between applying a texture and placing the complete geometry he had prepared. The floor was rebuilt using **19,564 complete `Panel1` instances across 17 zones**, at scale one; the ceiling received the same panel grid. This number is **not** presented as a count of individual actors.

Fire evolved from an effect rejected by the director for looking like a static image appearing and disappearing into a Niagara effect, first tested in one brazier and then expanded after review. At one stage, **13 fire effects** were recorded; a later stage contained **27 brazier lights at 4,500 lumens**. Lights and particle systems are not the same count, nor necessarily the same snapshot of the level.

Light intensity adjustments were hard to perceive while automatic exposure was interfering. Exposure for this pass was fixed at **EV100 = 2**, and the director evaluated the lighting changes. We do not attribute the entire visual result solely to a lumen value.

Editor blocks occurred because of the navigation ensure `Areas.Num() <= 1` in `RecastNavMeshGenerator.cpp`. Decorative elements participating in navigation were investigated; decoration components added during later work were configured not to affect NavMesh. **There is insufficient evidence to claim the underlying navigation issue was permanently fixed in general.** We do not hide that limitation behind a claim that the “map is stable forever.”

Severe loss of smoothness was also reported during the surface-covering pass. Documented optimization enabled Nanite on **13 meshes** and limited **36 textures to 1024**, while preserving protected resources and settings. Nanite optimizes geometry, not textures. The director reported improved smoothness, but there was no comparative benchmark and no proof that 4K textures were the sole cause. `Panel2` also retained a historical normals/binormals warning, not declared resolved without visual review.

#### 5. Making the game we could actually ship understandable

The director reviewed input mapping and resolved discrepancies among the instructions, implementation, and UI text. The final documented configuration in code and the controls screen was:

| Action | Final control |
|---|---|
| Move / camera | WASD or arrow keys / mouse |
| Jump | F |
| Sprint | Hold Space |
| Roll | Briefly press Space with a movement direction |
| Backstep | Briefly press Space without a movement direction |
| Light attack and combo | Left mouse button |
| Heavy attack | Shift + left mouse button |
| Charged attack | Hold left mouse button |
| Block | Hold right mouse button |
| Parry | Shift + right mouse button |
| Contextual critical | Left mouse button when an opportunity exists |
| Crouch / stand | C |
| Lock / unlock target | Q |
| Switch locked target | Mouse wheel |
| Heal | R |
| Interact / equip / pass through fog | E |
| Pause menu | Esc |

Changing buttons was not an opportunity to reconstruct combat. The lesson was particularly concrete: the director initially asked for a comparison of controls; modifying more than authorized and explaining progress poorly consumed time that should have gone into testing. A request to document buttons does not authorize changing a mechanic.

The tutorial began with movement, healing, and interaction. Approaching the initial enemy introduced crouching, lock-on, criticals, attacks, defense, and dodging. The language selector displayed visible **Español / English** buttons and stored the preference. Translations were added for the menus and prompts being worked on; this was **not** a comprehensive localization audit of every possible text in the game. Calling `SetCurrentCulture` could also change the editor's culture during in-editor tests; that side effect was acknowledged and was not claimed to be eliminated.

Pause was implemented with native UI: Esc opens Continue, Return to Main Menu, and Exit Game. Continuing restores gameplay input. In PIE, Esc also has the editor's normal behavior of ending the session, so an editor test does not replace testing the distributable executable. The agent performed neither visual test.

The final tutorial adjustment emphasized a mechanic that had not been explained: **Rally**. At the upper-left corner, a contrasting dark panel displays **“ESC — PAUSE MENU” for three seconds**, then changes to **“REGAIN HEALTH BY COUNTERATTACKING” for fifteen seconds**, explaining that striking within a short window after taking damage restores part of the lost health. Movement controls remain at the bottom to avoid covering the same space. Both prompts were prepared in Spanish and English. They were HUD instructions, not changes to Rally's underlying rules.

Healing started with **six charges** and a counter beside the health text, reusing the existing inventory. The counter included a reserved charge until consumption was confirmed; canceling before consumption should not subtract it. We did **not** implement item pickup or the previously proposed 40% drop chance: the director explicitly removed that scope. Nor do we claim to have completed a new layered walk-while-healing animation or a new policy to reserve all combo stamina in advance.

The ending preserved three steps: **NECOC YAOTL / Yaxché Industries**, a thank-you explaining that this was the first prototype created by a solo developer during the MegaJam, and the question:

> **What if we had managed to stop the invaders?**

This is the narrative closing of a fantasy work, a counterfactual question—not a proven historical claim.

#### 6. The last enemy was packaging

We used **Unreal Automation Tool, `RunUAT.bat BuildCookRun`, Windows x64, Shipping**. The process compiled C++, cooked, staged, packaged, and archived the game; included `L_MainMenu` and `L_RitualDungeon_Graybox`; and preserved the full Unreal distribution with executable, containers, and prerequisites. We did not merely zip the `.exe`.

Early attempts encountered two different blocks that should not be confused with gameplay errors: environment permissions to write logs under AppData, and UnrealBuildTool's **`Unable to build while Live Coding is active`**, exit code 6. The agent did not close the editor or force Hot Reload. Authorized retries continued after the director intervened. We did not switch to Development configuration to conceal a Shipping blocker.

The first package also exposed a missing dependency: **the menu background image existed in the project but was absent from the cook**. The code loaded it from a text path through `LoadObject`; that alone did not create the explicit package reference needed. We corrected this with a serialized reference to `T_MainMenu_Background`. The final package manifest contained it. ZIP integrity had not proven that this particular resource was included; the omission was a verification failure that needed correction.

Another source of confusion was announcing that changes had been saved and compiled for the editor while the director expected an updated ZIP. We clarified the distinction and packaged again with the latest Esc and Rally messages. The final deliverable was archived in the project's release directory.

**Verified technical results of the final package:**

| Check | Result |
|---|---|
| Unreal Automation Tool | `BUILD SUCCESSFUL`, exit code 0 |
| Platform / configuration | Win64 / Shipping |
| Entry executable | `Windows/NecocYaotl.exe` |
| Full distribution | 32 files; 1,103,357,244 bytes |
| ZIP | `NecocYaotl_Windows.zip`; 786,264,537 bytes |
| Integrity | Matching file list and sizes; correct CRC on every entry |
| Maps | Menu and temple verified in the manifest |
| Menu background | `T_MainMenu_Background.uasset` included in manifest |
| Dependencies | `.pak`, `.utoc`, `.ucas` containers and prerequisites present |
| Final tutorial | Rally text located in the Shipping binary |
| Agent-run execution test | Not performed |

Final ZIP SHA-256:

`c5f846298306e68645d74a47faf2d7d5eeb7e7896ca1f83ad63f4522f3bdd92f`

This checksum identifies the locally verified file. It does not mean the file was compared byte-for-byte with a download from itch.io. Playtesting the distributable executable remained exclusively the director's responsibility.

#### 7. Submission: leaving the editor and entering the competition

**REPORTED AND CONFIRMED BY THE DIRECTOR:** Necoc Yaotl was officially submitted to the **2026 Epic AI MegaJam on November 15**, **one hour and seven minutes before the deadline**. We do not derive an exact submission time or registration ID from that margin.

The Windows build was published on itch.io, gameplay footage was uploaded to YouTube, and the entry was submitted to the competition. This development journal was prepared for the Glass Box category. At the time of writing, these publication and submission details came from the director's confirmation; the review did not independently download the game, play the video, or retrieve an official receipt. No registration identifier or unverified submission details are asserted.

Delivery was no longer just a map open inside Unreal. There was a complete packaged Windows distribution and a public submission confirmed by the person who directed the work and performed its gameplay tests. That did not mean the prototype had become a finished commercial release.

#### 8. Who did what, and which resources predated the jam

**Eduardo Ortiz Quiroz, director of Yaxché Industries,** was the team's sole human developer. Responsibilities included vision, story, artistic and technical decisions, asset preparation and adjustments, prioritization, instructions, approvals, gameplay and visual testing, acceptance or rejection of results, and submission. AI agents were not counted as additional human team members.

**DeepSeek V4.1 Flash through OpenCode**, using the identifier from the director's original record, contributed foundational work, system implementation, import, technical preparation and integration, diagnostics, automation, and reporting in earlier milestones. We do not retroactively attribute that work to Codex or imply DeepSeek performed every later change.

**Codex (OpenAI)** contributed to final integration and stabilization: animation and transforms, the Conquistador and boss, defense adjustments, impact review and restoration after a failed integration, environment and lighting, controls, HUD and menus, compilation, and packaging. Its work also included scope errors, regressions, and insufficiently clear status reporting. We preserve those mistakes rather than make AI collaboration look perfect. During this phase, Codex performed static checks and compilation, not the visual validation reserved for the director.

**ChatGPT (OpenAI)** supported planning, alternative analysis, writing implementation instructions, reviewing proposals, conceptual research, coordination, and documentation. **Grok (xAI)** retains its historical role in Milestone 3's combat research and architecture; without evidence, it is not credited for final integrations.

**External resources and their actual timing:**

- **Quaternius:** Universal Animation Library and Universal Animation Library 2, locally checked as **CC0 1.0 Universal**. The source animations and base skeleton were not authored from scratch during the jam. The `NY_` prefix identifies project exports and integration, not original authorship of the movements. The 65 source bones and 66 imported entries (with an extra armature node) are not two separate original Skeletons. Crucially, the library was **not prepared or integrated for Necoc Yaotl before the jam**; its evaluation and technical adaptation took place during the competition.
- **WeLoveIndies:** third-party sound resources that already existed as a library, but were obtained during the jam, not stockpiled or integrated for Necoc Yaotl beforehand. The MegaJam arrangement described access for non-commercial use; **that is not a declaration that every sound is CC0**, nor automatic permission for future commercial exploitation. A complete audio file inventory and individual licenses remain to be confirmed.
- **Unreal Engine:** Manny/Quinn, template animations and resources temporarily used for testing, as well as runtime dependencies required by the distribution. Starting from templates does not mean we created their assets during the jam or reused an earlier game of our own.
- **Tripo and Blender:** the work described here involved generating, preparing, and adapting the protagonist, enemy, accessories, and architecture during development. AI-assisted generation is not the same as entirely manual modeling; installing or investigating a tool does not prove it produced a final asset. Rokoko and iClone experiments retain the limitations already stated in earlier milestones.

No original game-specific characters, environments, combat systems, or gameplay are presented as work completed before **November 12**. The third-party libraries existed independently, but choosing, adapting, and integrating them for Necoc Yaotl happened during the jam. We do not claim ownership of third-party catalogs or assign new licenses to the game, its models, or its code in this journal.

#### 9. Final reflection: what we finished and what remains

In four days we went from a basic project to a prototype with a distinctive Mexica identity, an adapted original protagonist and enemies, a temple, Rally-centered combat, defense and criticals, a boss, interface, tutorial, and Windows distribution. The official entry, according to the director's confirmation, was submitted before the deadline. That is the accomplishment. It does not need to be inflated by claiming every original idea was implemented.

The mistakes were part of the outcome too. Animation consumed more time than expected. Scale was compensated without structurally resolving its source. The first hitbox change damaged combat and had to be reverted. An image visible in the editor was missing from the first package. Debugging was essential to development but had to be turned off to judge the player experience. Agents sometimes took too long, misunderstood scope, or expressed certainty not supported by evidence. Human direction was indispensable to notice those failures, stop them, and decide what could wait.

We learned to distinguish **imported, connected, saved, compiled, packaged, and tested**. We also learned that a rollback can be the right kind of progress, that a small adjustment deserves a small solution, and that a final ZIP needs an unambiguous location, must reflect the last approved changes, and must be checked for dependencies—not merely pass a generic archive integrity test.

**Unfinished work and limits we do not hide:** structural normalization of the scale pipeline; deformation and transition polish; hit timing and contact requiring human validation; combat feel and behavior in groups; a generally verified solution for the navigation ensure; complete localization coverage; a detailed public audio inventory and licenses; independent verification of the entry receipt and public distribution; and executable runtime and compatibility testing that this technical review did not perform. Full integration of every library animation, consumable pickups, a new hitbox system, or advance reservation of all combo stamina do not become completed features merely because they appeared in a request.

The last Git commit recorded for this account of development was `21a5156`, dated November 14. Much of the November 15 work and this journal did not yet have a final delivery commit when the record was assembled. We preserve that limitation rather than imply that every last change is represented by a commit. This document is the development narrative itself; it does not imply that any separate evidence file or repository publication is already available.

**Result:** according to the director's confirmation, a first prototype was delivered, together with a journal that preserves the problems encountered along the way. Glass Box is an opportunity to show how we got there, not to erase what went wrong. The final cut still belongs to the director.
