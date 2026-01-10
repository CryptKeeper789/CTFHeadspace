#### Challenge information

# Where's the Artifact?

A notorious artifact collector, known only as "The Collector", has scattered fragments of a priceless relic across a network of unassuming web pages. Each page seems identical, a bland testament to digital monotony. However, hidden among them lies the final piece, the key to unlocking the relic's power.

Our intelligence suggests that The Collector's network is accessible, but subtly guarded. You will need to carefully examine each page, follow the links, and uncover the hidden artifact. Be warned: distractions abound. Most pages lead to dead ends.

#### The Challenge:

Navigate The Collector's web of deception. Your mission is to find the page containing the complete artifact - our elusive flag!

#### Hints

- Explore the links and find the flag hidden within one of the pages.
- The artifact is a carefully concealed piece of text, located within the body of one of the web pages.

**Good luck, agent. The fate of the relic is in your hands!**

## How I Cracked it:

**Note:** there were 5000 links on the main page that could have a flag. 

-  asked claude for help finding the flag. 
- asked the LLM to use binary search to reduce how long it took to catch the flag. 
- saved the code it gave me in a .py file in my CTF school folder. Opened terminal there and ran this code: `python artifact_bruteforce.py`
### Here is the Python code it generated:
#!/usr/bin/env python3
"""
Binary search approach for finding the artifact page
Much faster than linear scanning!
"""

import requests
import urllib3
import re
from bs4 import BeautifulSoup
import concurrent.futures
from threading import Lock

# Disable SSL warnings
urllib3.disable_warnings(urllib3.exceptions.InsecureRequestWarning)

class ArtifactFinder:
    def __init__(self, base_url):
        self.base_url = base_url
        self.found_flag = None
        self.lock = Lock()
        
    def check_page(self, page_num):
        """Check a single page for the artifact"""
        url = f"{self.base_url}/item/{page_num}"
        
        try:
            r = requests.get(url, verify=False, timeout=5)
            
            # Look for flag patterns
            flags = re.findall(r'(flag|FLAG|artifact|ARTIFACT)\{[^}]+\}', r.text, re.IGNORECASE)
            
            if flags:
                with self.lock:
                    if not self.found_flag:
                        self.found_flag = (page_num, flags[0], url)
                        print(f"\n{'='*70}")
                        print(f"🎯 FLAG FOUND!")
                        print(f"{'='*70}")
                        print(f"Page Number: {page_num}")
                        print(f"URL: {url}")
                        print(f"Flag: {flags[0]}")
                        print(f"{'='*70}\n")
                return True, flags[0]
            
            # Check if page says "Wrong Guess" vs something else
            soup = BeautifulSoup(r.text, 'html.parser')
            text = soup.get_text().strip().lower()
            
            # If it doesn't say "wrong guess", it might be special
            if "wrong guess" not in text and "not here" not in text:
                if "artifact" in text or "relic" in text or "collector" in text:
                    print(f"\n⚠️  Unusual content at page {page_num}: {url}")
                    print(f"Preview: {soup.get_text().strip()[:150]}...")
                    return True, None
                    
            return False, None
            
        except Exception as e:
            return False, None
    
    def parallel_search(self, start, end, chunk_size=50):
        """Search using parallel threads for speed"""
        print(f"\n🔍 Parallel searching pages {start} to {end}")
        print(f"Using {chunk_size} concurrent workers")
        print("=" * 70)
        
        pages_to_check = list(range(start, end + 1))
        checked = 0
        
        with concurrent.futures.ThreadPoolExecutor(max_workers=chunk_size) as executor:
            future_to_page = {executor.submit(self.check_page, page): page 
                            for page in pages_to_check}
            
            for future in concurrent.futures.as_completed(future_to_page):
                checked += 1
                if checked % 100 == 0:
                    print(f"Progress: {checked}/{len(pages_to_check)} pages checked...", end='\r')
                
                found, flag = future.result()
                if found and flag:
                    # Cancel remaining tasks
                    for f in future_to_page:
                        f.cancel()
                    return flag
        
        print(f"\nCompleted checking {checked} pages")
        return None
    
    def binary_search_pattern(self, start, end):
        """
        Use binary search logic to find patterns in page distribution
        Check middle points first to identify where the artifact might be
        """
        print(f"\n🎯 Binary Search Pattern: Checking strategic points")
        print("=" * 70)
        
        # Check key strategic points first
        strategic_points = [
            (start + end) // 2,  # Middle
            (start + (start + end) // 2) // 2,  # 1st quarter
            ((start + end) // 2 + end) // 2,  # 3rd quarter
            start,  # Start
            end,  # End
        ]
        
        print(f"Checking strategic points: {strategic_points}")
        
        for point in strategic_points:
            if start <= point <= end:
                print(f"Checking page {point}...")
                found, flag = self.check_page(point)
                if found and flag:
                    return flag
        
        return None
    
    def smart_search(self, start=1, end=5000):
        """
        Intelligent search strategy:
        1. Check strategic points first (binary search pattern)
        2. If not found, do parallel sweep
        """
        print("=" * 70)
        print("  SMART ARTIFACT SEARCH")
        print("=" * 70)
        print(f"Range: {start} to {end} ({end - start + 1} pages)")
        print("=" * 70)
        
        # Strategy 1: Binary search pattern for strategic points
        flag = self.binary_search_pattern(start, end)
        if flag:
            return flag
        
        print("\n❌ Not found in strategic points")
        print("📊 Starting full parallel sweep...")
        
        # Strategy 2: Full parallel search
        flag = self.parallel_search(start, end, chunk_size=50)
        
        if flag:
            return flag
        else:
            print("\n❌ No flag found in range")
            return None

def main():
    base_url = "https://90936bc9c0b60bf7d13bff3ca7ed46d0.challenge.hackazon.org"
    
    finder = ArtifactFinder(base_url)
    
    # Search pages 1 to 5000
    flag = finder.smart_search(1, 5000)
    
    if flag:
        print(f"\n✅ SUCCESS!")
        print(f"📍 Flag: {flag}")
    else:
        print("\n❌ Search complete - no flag found")
        print("Try:")
        print("  - Checking a different range")
        print("  - Looking at the actual page content manually")
        print("  - Verifying the challenge URL is correct")

if __name__ == "__main__":
    main()

### Output:
![[Pasted image 20260110125345.png]]