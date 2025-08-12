# data/skeleton.py
"""
SMPL-22 skeleton definitions and joint structures
"""

# SMPL-22 Joint Names
SMPL22_JOINT_NAMES = [
    "Hips",                  # 0 - ROOT
    "LeftUpLeg",             # 1 - Left Thigh
    "RightUpLeg",            # 2 - Right Thigh
    "Spine",                 # 3 - Lower Spine
    "LeftLeg",               # 4 - Left Knee
    "RightLeg",              # 5 - Right Knee
    "Spine1",                # 6 - Middle Spine
    "LeftFoot",              # 7 - Left Ankle
    "RightFoot",             # 8 - Right Ankle
    "Spine2",                # 9 - Upper Spine
    "LeftToe",               # 10 - Left Toe
    "RightToe",              # 11 - Right Toe
    "Neck",                  # 12 - Neck Base
    "LeftShoulder",          # 13 - Left Clavicle
    "RightShoulder",         # 14 - Right Clavicle
    "Head",                  # 15 - Head
    "LeftArm",               # 16 - Left Upper Arm
    "RightArm",              # 17 - Right Upper Arm
    "LeftForeArm",           # 18 - Left Elbow
    "RightForeArm",          # 19 - Right Elbow
    "LeftHand",              # 20 - Left Wrist
    "RightHand",             # 21 - Right Wrist
]

# SMPL-22 kinematic chains (bone connections)
SMPL22_KINEMATIC_CHAINS = [
    # Spine chain: Hips -> Spine -> Spine1 -> Spine2 -> Neck -> Head
    [0, 3, 6, 9, 12, 15],
    
    # Left leg: Hips -> LeftUpLeg -> LeftLeg -> LeftFoot -> LeftToe
    [0, 1, 4, 7, 10],
    
    # Right leg: Hips -> RightUpLeg -> RightLeg -> RightFoot -> RightToe  
    [0, 2, 5, 8, 11],
    
    # Left arm: Spine2 -> LeftShoulder -> LeftArm -> LeftForeArm -> LeftHand
    [9, 13, 16, 18, 20],
    
    # Right arm: Spine2 -> RightShoulder -> RightArm -> RightForeArm -> RightHand
    [9, 14, 17, 19, 21]
]
