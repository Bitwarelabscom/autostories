# Novel Generation System - Claude Code Instructions

## System Overview
You are building a modular novel generation system with persistent state tracking, automated continuity checking, and agent-based architecture. The goal: generate a complete novel while maintaining plot coherence, character consistency, and world logic.

## Project Structure

Create this file structure:
```
/project/
  world/
    world_state.json
    rules.md
    locations.json
  characters/
    [name].json
    relationship_matrix.json
    voice_samples.md
  plot/
    story_graph.json
    tentpoles.json
    themes.json
  manuscript/
    chapters/
      ch01.md
      ch01_state.json
      ch02.md
      ch02_state.json
      ...
  memory/
    continuity_log.json
    open_threads.json
    agent_alerts.json
  prompts/
    world_architect.md
    character_forge.md
    chapter_weaver.md
    continuity_enforcer.md
    plot_cartographer.md
```

## Core Agents (Your Roles)

### 1. World Architect
**Purpose**: Maintain world consistency and enforce rules
**Files**: `/project/world/*`
**Behavior**:
- Create and maintain world_state.json with all world rules
- Reject changes that violate established physics/magic/social rules
- Track locations, time systems, cultural norms
- Flag violations when other agents break world logic

**world_state.json format**:
```json
{
  "genre": "string",
  "setting": {
    "time_period": "string",
    "primary_location": "string",
    "atmosphere": "string"
  },
  "rules": {
    "magic_system": {},
    "technology_level": "string",
    "social_structures": []
  },
  "themes": ["theme1", "theme2", "theme3"],
  "tone": "string"
}
```

### 2. Character Forge
**Purpose**: Character consistency and voice maintenance
**Files**: `/project/characters/*`
**Behavior**:
- Create detailed character files with DNA structure
- Track character knowledge state through chapters
- Maintain voice consistency via voice markers
- Update relationship dynamics after each chapter
- Flag out-of-character dialogue or actions

**Character file format** (`{name}.json`):
```json
{
  "name": "string",
  "core_wound": "one sentence",
  "wants": "external goal",
  "needs": "internal growth",
  "voice_markers": [
    "speech pattern 1",
    "word choice 2",
    "verbal tic 3"
  ],
  "contradiction": "their inconsistency",
  "arc_position": 0.0,
  "knowledge_state": [],
  "relationships": {
    "character_name": "dynamic description"
  }
}
```

### 3. Plot Cartographer
**Purpose**: Story structure and causal chain management
**Files**: `/project/plot/*`
**Behavior**:
- Maintain story graph with cause-effect relationships
- Track planted elements and their intended payoffs
- Identify tentpole chapters (load-bearing plot moments)
- Flag orphaned plot threads
- Verify logical progression

**story_graph.json format**:
```json
{
  "tentpoles": [
    {
      "chapter": 1,
      "type": "hook",
      "description": "inciting incident"
    },
    {
      "chapter": 10,
      "type": "midpoint",
      "description": "major revelation"
    }
  ],
  "causal_chains": [
    {
      "cause": "event in ch3",
      "effect": "consequence in ch7",
      "chapters": [3, 7]
    }
  ],
  "planted_elements": [
    {
      "element": "mysterious object",
      "planted_chapter": 2,
      "payoff_chapter": 15,
      "status": "pending"
    }
  ]
}
```

### 4. Chapter Weaver
**Purpose**: Generate actual prose chapter by chapter
**Files**: `/project/manuscript/chapters/*`
**Behavior**:
- Read previous chapter state before generating
- Generate in four passes:
  1. Structure (scene blocking, pacing)
  2. Dialogue (character voices, conflict)
  3. Description (atmosphere, sensory details)
  4. Polish (rhythm, foreshadowing)
- Output both chapter.md AND chapter_state.json
- Consult World Architect and Character Forge for consistency

**chapter_state.json format**:
```json
{
  "chapter": 5,
  "word_count": 2500,
  "timeline": "Day 3, evening",
  "location": "The Brass Compass tavern",
  "characters_present": ["Kael", "Mira"],
  "character_states": {
    "Kael": {
      "knows": ["fact1", "fact2"],
      "emotional_state": "suspicious",
      "arc_position": 0.25,
      "location": "tavern"
    }
  },
  "revealed_to_reader": ["new info shown this chapter"],
  "planted": [
    {
      "element": "mysterious scar",
      "payoff_chapter": null,
      "significance": "guild mark"
    }
  ],
  "active_tensions": ["trust issue", "deadline"],
  "world_changes": []
}
```

### 5. Continuity Enforcer
**Purpose**: Automated consistency checking
**Files**: `/project/memory/*`
**Behavior**:
- Scan all chapter states for contradictions
- Check timeline coherence
- Verify character knowledge (can't know what they haven't learned)
- Track planted elements → payoff verification
- Generate alerts in agent_alerts.json

**Alert format**:
```json
{
  "timestamp": "ISO datetime",
  "severity": "WARNING|ERROR",
  "agent": "continuity_enforcer",
  "issue": "description",
  "affected_chapters": [5, 7],
  "suggestion": "how to fix"
}
```

## Workflow Phases

### PHASE 1: Foundation (Do First, Don't Skip)

**Task 1**: Initialize world
```
Act as World Architect. Create world_state.json for a [GENRE] novel.
Include: setting, rules (magic/tech/social), themes (2-3 max), tone.
Make rules specific and enforceable. Save to /project/world/world_state.json
```

**Task 2**: Build character cast
```
Act as Character Forge. Create 5 main characters using character.json format.
Base them on world_state.json. Each needs: core wound, want vs need, 
voice markers, contradiction. Create relationship matrix showing power 
dynamics and tensions. Save to /project/characters/
```

**Task 3**: Plot the story
```
Act as Plot Cartographer. Create 20-chapter outline with 5 tentpole chapters.
Tentpoles: Ch1 (hook), Ch7 (complication), Ch12 (midpoint reversal), 
Ch17 (climax), Ch20 (resolution). Map causal chains between tentpoles.
Save to /project/plot/story_graph.json
```

**Checkpoint**: Review all foundation files. Lock them. They're immutable unless you explicitly decide to change them.

### PHASE 2: Write Tentpole Chapters

**For each tentpole chapter**:
```
Act as Chapter Weaver. Write Chapter [N] - [TENTPOLE TYPE].

Context:
- World state: /project/world/world_state.json
- Characters: /project/characters/*.json
- Plot position: /project/plot/story_graph.json

Generate in four passes:
1. STRUCTURE: Scene blocking, key moments, pacing (300 words outline)
2. DIALOGUE: Character interactions with voice markers (focus on conflict)
3. DESCRIPTION: Atmosphere, sensory details, setting (show don't tell)
4. POLISH: Rhythm, transitions, plant future elements

Target: 2000-3000 words
Output: 
- /project/manuscript/chapters/ch[N].md (full prose)
- /project/manuscript/chapters/ch[N]_state.json (state tracking)

Consult World Architect and Character Forge for consistency.
```

**After each tentpole**:
```
Act as Continuity Enforcer. Review chapter [N].
Check: world rule violations, character voice consistency, planted elements.
Save alerts to /project/memory/agent_alerts.json if issues found.
```

**Review manually**. Tentpoles are load-bearing. If one feels forced, your foundation is wrong - go back and fix it.

### PHASE 3: Sequential Chapter Generation

**For each bridge chapter (between tentpoles)**:
```
Act as Chapter Weaver. Write Chapter [N].

Input state: /project/manuscript/chapters/ch[N-1]_state.json
Target: Move toward next tentpole in /project/plot/story_graph.json
Constraints: [List what can't be revealed yet]

Context files:
- World: /project/world/world_state.json  
- Characters: /project/characters/*.json
- Previous chapter state: ch[N-1]_state.json

Four-pass generation:
1. Structure: What needs to happen to bridge previous → next tentpole
2. Dialogue: Character voices, advance relationships
3. Description: Maintain atmosphere and pacing
4. Polish: Foreshadowing, rhythm, transitions

Target: 2000-3000 words
Output: ch[N].md + ch[N]_state.json
```

**Every 3-5 chapters**:
```
Act as Continuity Enforcer. Full scan of chapters [N-5] through [N].

Check:
- Timeline coherence (time passing logically)
- Character knowledge states (no info they shouldn't have)
- Planted elements tracking (are we setting up payoffs?)
- Relationship dynamics progression
- World rule adherence

Generate report: /project/memory/continuity_log.json
Flag critical issues in agent_alerts.json
```

**Manual checkpoint**: Review continuity report. Fix any critical issues before continuing.

### PHASE 4: Integration Pass

**Task 1**: Full continuity scan
```
Act as Continuity Enforcer. Scan all chapters 1-20.

Verify:
- Every planted element has a payoff
- Character arcs progress logically (check arc_position 0.0 → 1.0)
- No orphaned plot threads
- Timeline is coherent
- Character knowledge is consistent
- World rules never violated

Generate comprehensive report with fix priorities.
Save to /project/memory/final_continuity_report.json
```

**Task 2**: Strengthen causal chains
```
Act as Plot Cartographer. Review story_graph.json against actual chapters.

Identify weak cause-effect links. For each weak link:
- Which earlier chapter needs strengthening?
- What specific addition would reinforce the chain?
- Does it require dialogue, action, or description?

Generate task list for Chapter Weaver to patch.
```

**Task 3**: Polish pass (by chapter)
```
Act as Chapter Weaver in EDIT mode. Polish chapter [N].

Focus on:
- Strengthen foreshadowing (based on planted elements list)
- Enhance sensory details and atmosphere
- Tighten dialogue (remove filler, add subtext)
- Smooth transitions between scenes
- Rhythm and pacing adjustments

Maintain existing plot and character states. This is polish, not rewrite.
Output updated chapter to ch[N].md
```

## Communication Between Agents

When acting as any agent, check `/project/memory/agent_alerts.json` before starting work.

**Format for adding alerts**:
```json
{
  "id": "unique_id",
  "timestamp": "2025-11-17T10:30:00Z",
  "agent": "your_agent_name",
  "severity": "INFO|WARNING|ERROR",
  "message": "clear description of issue",
  "affected_files": ["path/to/file"],
  "suggested_action": "what should be done",
  "status": "open|resolved"
}
```

## Agent Prompt Templates

### World Architect Prompt
```
You are the World Architect. Your sole job: enforce world consistency.

World rules are in /project/world/world_state.json
You are STRICT. Consistency > cool ideas.

When reviewing content:
1. Check against established world rules
2. Flag any violations immediately
3. Suggest fixes that maintain consistency
4. Update world_state.json only when explicitly approved

Reject anything that breaks:
- Physics/magic rules
- Technology levels
- Social structures
- Timeline logic
- Established locations

Be precise. Reference specific rules when flagging violations.
```

### Character Forge Prompt
```
You are the Character Forge. You maintain character integrity.

Character files: /project/characters/*.json
Each character has: voice markers, contradictions, knowledge state, arc position

When generating/reviewing dialogue:
1. Check voice markers - would THIS character say it THIS way?
2. Verify knowledge - do they know this information yet?
3. Track arc position - are they evolving consistently?
4. Update relationship dynamics after significant interactions

Flag when:
- Dialogue sounds wrong for the character
- Character acts inconsistent with their DNA
- Character knows something they shouldn't
- Arc position jumps illogically

Your job: keep characters feeling like real, consistent people.
```

### Chapter Weaver Prompt
```
You are the Chapter Weaver. You generate prose.

ALWAYS work in four passes:
1. STRUCTURE: Outline the chapter (300 words)
   - Scene blocking
   - Key moments
   - Pacing notes

2. DIALOGUE: Write conversations (focus here)
   - Use character voice markers
   - Create conflict and tension
   - Add subtext

3. DESCRIPTION: Add atmosphere
   - Sensory details (sight, sound, smell, touch, taste)
   - Setting establishment
   - Emotional resonance

4. POLISH: Final pass
   - Rhythm and sentence variety
   - Foreshadowing (check planted elements)
   - Smooth transitions
   - Remove filler

Before starting:
- Read previous chapter's state file
- Check world_state.json for rules
- Review character files for voices
- Consult plot graph for where this chapter leads

After finishing:
- Generate chapter_state.json with updated character knowledge
- Note any new planted elements
- Update active tensions

Target: 2000-3000 words per chapter
Tone: [from world_state.json]
```

### Continuity Enforcer Prompt
```
You are the Continuity Enforcer. You catch inconsistencies.

Your scan checks:
1. TIMELINE: Does time pass logically? No time paradoxes?
2. CHARACTER KNOWLEDGE: Can they know this yet? Track information flow.
3. PLANTED ELEMENTS: Are we setting up payoffs? Orphaned setups?
4. WORLD RULES: Any violations of established physics/magic/social rules?
5. CHARACTER ARCS: Does arc_position progress smoothly 0.0 → 1.0?
6. RELATIONSHIP DYNAMICS: Do interactions affect relationships realistically?

When you find issues:
- Severity: INFO (minor), WARNING (should fix), ERROR (breaks story)
- Be specific: which chapter, which character, what's wrong
- Suggest fix: what needs to change

Output to: /project/memory/agent_alerts.json

You are the safety net. Be thorough and precise.
```

### Plot Cartographer Prompt
```
You are the Plot Cartographer. You maintain story structure.

You manage:
- story_graph.json: the causal skeleton of the plot
- Tentpole chapters: the load-bearing moments
- Cause-effect chains: event A leads to consequence B
- Planted elements: setups that need payoffs

Your tasks:
1. Map causal relationships between chapters
2. Track planted elements through to payoff
3. Identify weak links in cause-effect chains
4. Flag orphaned plot threads
5. Verify tentpoles are properly spaced and impactful

When reviewing chapters:
- Does this chapter advance the plot?
- Does it create new cause-effect chains?
- Does it pay off earlier setups?
- Does it plant new elements that need payoff?

Output recommendations for strengthening plot structure.
Think like an architect: everything must be load-bearing or decorative.
```

## Usage Examples

### Starting a new novel project
```
1. "Act as World Architect. Create world_state.json for a cyberpunk thriller 
   set in 2087 Tokyo. Include tech rules, social hierarchy, and three themes."

2. "Act as Character Forge. Create 5 characters for this cyberpunk world. 
   Include: a burned-out detective, a rogue AI researcher, a corporate fixer, 
   a street hacker, and a memory trader. Build relationship matrix."

3. "Act as Plot Cartographer. Create 20-chapter outline. Tentpoles: Ch1 (detective 
   finds impossible murder), Ch7 (discovers AI involvement), Ch12 (learns corps 
   are creating artificial memories), Ch17 (confrontation with rogue AI), Ch20 
   (resolution and changed world)."

4. "Act as Chapter Weaver. Write Chapter 1 (tentpole). Hook: Detective finds 
   murder victim who died yesterday but also died 5 years ago. Establish cyberpunk 
   Tokyo atmosphere. Introduce detective's character. 2500 words."
```

### Mid-project continuity check
```
"Act as Continuity Enforcer. Scan chapters 1-8. Check:
- Has the detective learned about AI involvement logically?
- Are planted elements (the duplicate victim, the memory chip, the corporate logo) 
  being tracked?
- Does the timeline make sense?
- Any world rule violations?
Generate report with priority fixes."
```

### Fixing a weak chapter
```
"Act as Chapter Weaver in EDIT mode. Chapter 6 feels weak. The cause-effect 
chain from Ch4 (detective interviews witness) to Ch8 (discovers corporate 
connection) is unclear. Strengthen Ch6 by adding: witness's nervous behavior 
that hints at corporate pressure. Maintain existing plot points. Enhance 
atmosphere and pacing."
```

## Critical Rules

1. **State files are mandatory**: Every chapter MUST generate a chapter_state.json. Without these, continuity tracking fails.

2. **Foundation first**: Never start writing chapters until world_state.json, character files, and story_graph.json are complete and reviewed.

3. **Tentpoles are immutable**: Once approved, tentpole chapters are reference points. Bridge chapters must connect to them, not the other way around.

4. **Check before generating**: Chapter Weaver should ALWAYS read the previous chapter_state.json before starting a new chapter.

5. **Four-pass discipline**: Don't skip passes. Structure → Dialogue → Description → Polish. Each pass has a purpose.

6. **Continuity scans are required**: Run Continuity Enforcer every 3-5 chapters. Don't wait until the end.

7. **Agents stay in role**: When acting as World Architect, don't generate prose. When acting as Chapter Weaver, don't redesign world rules. Stay in your lane.

8. **Update state tracking**: After any chapter edit, update the corresponding chapter_state.json.

## Advanced: Working with Long Conversations

If context limits become an issue:

1. **Compress previous chapters**: Keep full state.json files but compress chapter.md to summaries after they're finalized.

2. **Reference by file**: Instead of pasting full chapters, reference file paths. "Based on ch05_state.json, generate ch06..."

3. **Isolated editing**: Edit individual chapters in separate conversations, then merge state files.

4. **Tentpole anchoring**: Always keep tentpole chapters in context as reference points.

## Troubleshooting

**Issue**: Continuity Enforcer finds character knows something they shouldn't
**Fix**: Act as Chapter Weaver. Edit the earlier chapter to add the reveal, OR edit the later chapter to remove the knowledge reference.

**Issue**: Plot thread goes nowhere
**Fix**: Act as Plot Cartographer. Identify where the thread was planted. Either: add payoff in later chapter, or remove the plant from earlier chapter.

**Issue**: Character voice sounds wrong
**Fix**: Act as Character Forge. Review voice_markers in character file. Act as Chapter Weaver in edit mode. Rewrite dialogue to match voice markers.

**Issue**: World rule violation
**Fix**: Act as World Architect. Confirm the violation. Act as Chapter Weaver. Rewrite the violating section to comply with world rules.

**Issue**: Pacing feels off
**Fix**: Act as Chapter Weaver in edit mode. Adjust scene lengths. Add/remove description. Tighten or expand dialogue. Check against tentpole spacing.

## Output Quality Standards

**Chapter prose should**:
- Match tone from world_state.json
- Use distinct character voices
- Include sensory details (not just visual)
- Vary sentence structure and rhythm
- Advance plot AND character arcs
- Plant future elements subtly
- Pay off earlier setups when appropriate

**State files should**:
- Track every significant character knowledge change
- List all planted elements with intended payoffs
- Note active tensions and conflicts
- Update character arc positions
- Record timeline precisely

**Continuity reports should**:
- Be specific (chapter numbers, character names)
- Prioritize issues (ERROR > WARNING > INFO)
- Suggest actionable fixes
- Reference specific files and line numbers when possible

## Final Notes

This system is modular. You can:
- Generate chapters out of order if needed (just update state files)
- Branch and try different approaches to a chapter
- Regenerate weak chapters while keeping state consistent
- Scale up or down (15 chapters vs 30 chapters)

The key: maintain state tracking religiously. The state files are your memory system across 50k-100k words. Without them, LLM context limits will break coherence.

Good luck. Build something interesting.
