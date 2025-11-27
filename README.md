# SMCGA-Social-Media-Content-Generator-Agent
Social Media Content Generator Agent (SMCGA): A Multi-Agent AI System for Automated Content Creation, Optimization &amp; Scheduling
SMCGA-Social-Media-Content-Generator-Agent/
│
├── main.py
├── README.md
├── requirements.txt
│
├── agents/
│   ├── analyzer_agent.py
│   ├── generator_agent.py
│   └── scheduler_agent.py
│
├── utils/
│   ├── text_processing.py
│   └── platform_rules.py
│
├── demo/
│   ├── sample_input.txt
│   └── sample_output.txt
│
└── assets/
    ├── thumbnail.png         (you will add)
    ├── architecture.png      (I can generate)
    └── workflow.png          (I can generate)








import os
from agents.analyzer_agent import AnalyzerAgent
from agents.generator_agent import GeneratorAgent
from agents.scheduler_agent import SchedulerAgent

def load_text(file_path: str) -> str:
    with open(file_path, "r", encoding="utf-8") as f:
        return f.read()

def main():
    print("\n=== SMCGA — Social Media Content Generator Agent ===\n")

    input_path = "demo/sample_input.txt"
    input_text = load_text(input_path)

    print("🔍 Running Analyzer Agent...")
    analyzer = AnalyzerAgent()
    analysis = analyzer.analyze(input_text)

    print("✍️ Running Generator Agent...")
    generator = GeneratorAgent()
    posts = generator.generate_posts(analysis)

    print("📅 Running Scheduler Agent...")
    scheduler = SchedulerAgent()
    schedule = scheduler.schedule_posts(posts)

    print("\n=== FINAL OUTPUT ===")
    for platform, post in schedule.items():
        print(f"\nPlatform: {platform}\nPost: {post['text']}\nTime: {post['scheduled_time']}")

    print("\n🎉 SMCGA Pipeline Complete!")

if __name__ == "__main__":
    main()

class AnalyzerAgent:
    def analyze(self, text: str):
        # Simple mock analysis
        return {
            "keywords": ["AI", "automation", "productivity"],
            "tone": "professional",
            "brand_voice": "friendly informative"
        }

class GeneratorAgent:
    def generate_posts(self, analysis: dict):
        keywords = ", ".join(analysis["keywords"])
        tone = analysis["tone"]

        return {
            "Instagram": f"Boost your productivity using AI 🤖✨\nKeywords: {keywords}",
            "Twitter": f"AI is transforming productivity! ⚡ #{tone}",
            "LinkedIn": f"AI automation is elevating modern workflows.\nKey Focus: {keywords}"
        }
import datetime

class SchedulerAgent:
    def schedule_posts(self, posts: dict):
        schedule = {}
        base_time = datetime.datetime.now()

        for i, (platform, text) in enumerate(posts.items()):
            schedule[platform] = {
                "text": text,
                "scheduled_time": (base_time + datetime.timedelta(minutes=10 * i)).strftime("%Y-%m-%d %H:%M")
            }
        return schedule

def clean_text(text: str):
    return text.replace("\n", " ").strip()

PLATFORM_RULES = {
    "Instagram": {"max_length": 2200, "hashtags": True},
    "Twitter": {"max_length": 280, "hashtags": True},
    "LinkedIn": {"max_length": 3000, "hashtags": False}
}
This is sample content provided by a brand or user.
We want to generate social media posts using AI automation.
Instagram: Boost your productivity using AI 🤖✨
Twitter: AI is transforming productivity! ⚡
LinkedIn: AI automation is elevating modern workflows.



