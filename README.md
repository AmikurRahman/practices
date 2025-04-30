# practices

##code :

import random


def multiply(numbers):
    ans = 1
    for x in numbers:
          ans = ans * x

    return ans


def make_random_list(k):
    return [random.randint(1, 9) for _ in range(k)]

def change_one_number(numbers):
    pos = random.randint(0, len(numbers)-1)
    numbers[pos] = random.randint(1, 9)


def mix_lists(list1, list2):
    cut = random.randint(1, len(list1)-1)
    return list1[:cut] + list2[cut:]

def find_answer(T, k):
    lists = [make_random_list(k) for _ in range(100)]
    
    for _ in range(1000):
        lists.sort(key=lambda x: -abs(multiply(x) - T))

        
        if multiply(lists[0]) == T:
            return lists[0]
        
        new_lists = lists[:10]
        
        while len(new_lists) < 100:
            a = random.choice(lists[:50])
            b = random.choice(lists[:50])
            
            new_list = mix_lists(a, b)
            
            if random.random() < 0.2:
                change_one_number(new_list)
            

            new_lists.append(new_list)
        
        lists = new_lists
    
    return None



T1, k1 = 12, 3
ans1 = find_answer(T1, k1)
print("Case #1 Output:", *ans1 if ans1 else "No solution")



T2, k2 = 18, 3
ans2 = find_answer(T2, k2)
print("Case #2 Output:", *ans2 if ans2 else "No solution")
